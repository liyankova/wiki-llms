---
url: https://bun.com/reference/node/stream
title: Node.js stream module | API Reference | Bun
source_domain: bun.com
---

# Node.js stream module | API Reference | Bun

Node.js module

# [stream](https://bun.com/reference/node/stream)

The `'node:stream'` module provides the API for working with streaming data in Node.js, including readable, writable, duplex, and transform streams.

Streams are event emitters that process data in chunks, offering memory-efficient handling of large data flows, such as file reading/writing and network communication.

Works in Bun

Fully implemented.

* ### [export default namespace stream](https://bun.com/reference/node/stream/default)

  + function [finished](https://bun.com/reference/node/stream/default/finished)(

    stream: ReadWriteStream | ReadableStream | WritableStream,

    options: [FinishedOptions](https://bun.com/reference/node/stream/default/FinishedOptions),

    callback: (err?: null | ErrnoException) => void

    ): () => void;

    A readable and/or writable stream/webstream.

    A function to get notified when a stream is no longer readable, writable or has experienced an error or a premature close event.

    ```
    import { finished } from 'node:stream';
    import fs from 'node:fs';

    const rs = fs.createReadStream('archive.tar');

    finished(rs, (err) => {
      if (err) {
        console.error('Stream failed.', err);
      } else {
        console.log('Stream is done reading.');
      }
    });

    rs.resume(); // Drain the stream.
    ```

    Especially useful in error handling scenarios where a stream is destroyed prematurely (like an aborted HTTP request), and will not emit `'end'` or `'finish'`.

    The `finished` API provides [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streamfinishedstream-options).

    `stream.finished()` leaves dangling event listeners (in particular `'error'`, `'end'`, `'finish'` and `'close'`) after `callback` has been invoked. The reason for this is so that unexpected `'error'` events (due to incorrect stream implementations) do not cause unexpected crashes. If this is unwanted behavior then the returned cleanup function needs to be invoked in the callback:

    ```
    const cleanup = finished(rs, (err) => {
      cleanup();
      // ...
    });
    ```

    @param stream

    A readable and/or writable stream.

    @param callback

    A callback function that takes an optional error argument.

    @returns

    A cleanup function which removes all registered listeners.

    function [finished](https://bun.com/reference/node/stream/default/finished)(

    stream: ReadWriteStream | ReadableStream | WritableStream,

    callback: (err?: null | ErrnoException) => void

    ): () => void;

    A readable and/or writable stream/webstream.

    A function to get notified when a stream is no longer readable, writable or has experienced an error or a premature close event.

    ```
    import { finished } from 'node:stream';
    import fs from 'node:fs';

    const rs = fs.createReadStream('archive.tar');

    finished(rs, (err) => {
      if (err) {
        console.error('Stream failed.', err);
      } else {
        console.log('Stream is done reading.');
      }
    });

    rs.resume(); // Drain the stream.
    ```

    Especially useful in error handling scenarios where a stream is destroyed prematurely (like an aborted HTTP request), and will not emit `'end'` or `'finish'`.

    The `finished` API provides [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streamfinishedstream-options).

    `stream.finished()` leaves dangling event listeners (in particular `'error'`, `'end'`, `'finish'` and `'close'`) after `callback` has been invoked. The reason for this is so that unexpected `'error'` events (due to incorrect stream implementations) do not cause unexpected crashes. If this is unwanted behavior then the returned cleanup function needs to be invoked in the callback:

    ```
    const cleanup = finished(rs, (err) => {
      cleanup();
      // ...
    });
    ```

    @param stream

    A readable and/or writable stream.

    @param callback

    A callback function that takes an optional error argument.

    @returns

    A cleanup function which removes all registered listeners.

    ### namespace [finished](https://bun.com/reference/node/stream/default/finished)
  + function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    transform3: T3,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, T4 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T3, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    transform3: T3,

    transform4: T4,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)(

    streams: readonly ReadWriteStream | ReadableStream | WritableStream[],

    callback: (err: null | ErrnoException) => void

    ): WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)(

    stream1: ReadableStream,

    stream2: ReadWriteStream | WritableStream,

    ...streams: ReadWriteStream | WritableStream | (err: null | ErrnoException) => void[]

    ): WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    ### namespace [pipeline](https://bun.com/reference/node/stream/default/pipeline)
  + ### class [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    Duplex streams are streams that implement both the `Readable` and `Writable` interfaces.

    Examples of `Duplex` streams include:

    - `TCP sockets`
    - `zlib streams`
    - `crypto streams`

    - [allowHalfOpen](https://bun.com/reference/node/stream/default/Duplex/allowHalfOpen): boolean

      If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

      This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
    - readonly [closed](https://bun.com/reference/node/stream/default/Duplex/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/stream/default/Duplex/destroyed): boolean

      Is `true` after `readable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/stream/default/Duplex/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - [readable](https://bun.com/reference/node/stream/default/Duplex/readable): boolean

      Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
    - readonly [readableAborted](https://bun.com/reference/node/stream/default/Duplex/readableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'end'`.
    - readonly [readableDidRead](https://bun.com/reference/node/stream/default/Duplex/readableDidRead): boolean

      Returns whether `'data'` has been emitted.
    - readonly [readableEncoding](https://bun.com/reference/node/stream/default/Duplex/readableEncoding): null | BufferEncoding

      Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
    - readonly [readableEnded](https://bun.com/reference/node/stream/default/Duplex/readableEnded): boolean

      Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
    - readonly [readableFlowing](https://bun.com/reference/node/stream/default/Duplex/readableFlowing): null | boolean

      This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
    - readonly [readableHighWaterMark](https://bun.com/reference/node/stream/default/Duplex/readableHighWaterMark): number

      Returns the value of `highWaterMark` passed when creating this `Readable`.
    - readonly [readableLength](https://bun.com/reference/node/stream/default/Duplex/readableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [readableObjectMode](https://bun.com/reference/node/stream/default/Duplex/readableObjectMode): boolean

      Getter for the property `objectMode` of a given `Readable` stream.
    - readonly [writable](https://bun.com/reference/node/stream/default/Duplex/writable): boolean

      Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
    - readonly [writableAborted](https://bun.com/reference/node/stream/default/Duplex/writableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'finish'`.
    - readonly [writableCorked](https://bun.com/reference/node/stream/default/Duplex/writableCorked): number

      Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
    - readonly [writableEnded](https://bun.com/reference/node/stream/default/Duplex/writableEnded): boolean

      Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
    - readonly [writableFinished](https://bun.com/reference/node/stream/default/Duplex/writableFinished): boolean

      Is set to `true` immediately before the `'finish'` event is emitted.
    - readonly [writableHighWaterMark](https://bun.com/reference/node/stream/default/Duplex/writableHighWaterMark): number

      Return the value of `highWaterMark` passed when creating this `Writable`.
    - readonly [writableLength](https://bun.com/reference/node/stream/default/Duplex/writableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [writableNeedDrain](https://bun.com/reference/node/stream/default/Duplex/writableNeedDrain): boolean

      Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
    - readonly [writableObjectMode](https://bun.com/reference/node/stream/default/Duplex/writableObjectMode): boolean

      Getter for the property `objectMode` of a given `Writable` stream.
    - static [captureRejections](https://bun.com/reference/node/stream/default/Duplex/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/Duplex/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/stream/default/Duplex/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/stream/default/Duplex/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [\_construct](https://bun.com/reference/node/stream/default/Duplex/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/stream/default/Duplex/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_final](https://bun.com/reference/node/stream/default/Duplex/_final)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_read](https://bun.com/reference/node/stream/default/Duplex/_read)(

      size: number

      ): void;
    - [\_write](https://bun.com/reference/node/stream/default/Duplex/_write)(

      chunk: any,

      encoding: BufferEncoding,

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_writev](https://bun.com/reference/node/stream/default/Duplex/_writev)(

      chunks: { chunk: any; encoding: BufferEncoding }[],

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/default/Duplex/[asyncDispose])(): Promise<void>;

      Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/default/Duplex/[asyncIterator])(): AsyncIterator<any>;

      @returns

      `AsyncIterator` to fully consume the stream.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/Duplex/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'close',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'drain',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'end',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'finish',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'pause',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'readable',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'resume',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Duplex/addListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe
    - [asIndexedPairs](https://bun.com/reference/node/stream/default/Duplex/asIndexedPairs)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

      @returns

      a stream of indexed pairs.
    - [compose](https://bun.com/reference/node/stream/default/Duplex/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [cork](https://bun.com/reference/node/stream/default/Duplex/cork)(): void;

      The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

      The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

      See also: `writable.uncork()`, `writable._writev()`.
    - [destroy](https://bun.com/reference/node/stream/default/Duplex/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `readable._destroy()`.

      @param error

      Error which will be passed as payload in `'error'` event
    - [drop](https://bun.com/reference/node/stream/default/Duplex/drop)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks dropped from the start.

      @param limit

      the number of chunks to drop from the readable.

      @returns

      a stream with *limit* chunks dropped from the start.
    - [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'close'

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

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'data',

      chunk: any

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'drain'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'end'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'error',

      err: [Error](https://bun.com/reference/globals/Error)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'finish'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'pause'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'pipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'readable'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'resume'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: 'unpipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Duplex/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [end](https://bun.com/reference/node/stream/default/Duplex/end)(

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      [end](https://bun.com/reference/node/stream/default/Duplex/end)(

      chunk: any,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      [end](https://bun.com/reference/node/stream/default/Duplex/end)(

      chunk: any,

      encoding: BufferEncoding,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding if `chunk` is a string
    - [eventNames](https://bun.com/reference/node/stream/default/Duplex/eventNames)(): string | symbol[];

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
    - [every](https://bun.com/reference/node/stream/default/Duplex/every)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
    - [filter](https://bun.com/reference/node/stream/default/Duplex/filter)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

      @param fn

      a function to filter chunks from the stream. Async or not.

      @returns

      a stream filtered with the predicate *fn*.
    - [find](https://bun.com/reference/node/stream/default/Duplex/find)<T>(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<undefined | T>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

      [find](https://bun.com/reference/node/stream/default/Duplex/find)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<any>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
    - [flatMap](https://bun.com/reference/node/stream/default/Duplex/flatMap)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

      It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

      @param fn

      a function to map over every chunk in the stream. May be async. May be a stream or generator.

      @returns

      a stream flat-mapped with the function *fn*.
    - [forEach](https://bun.com/reference/node/stream/default/Duplex/forEach)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<void>;

      This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

      This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

      This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise for when the stream has finished.
    - [getMaxListeners](https://bun.com/reference/node/stream/default/Duplex/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [isPaused](https://bun.com/reference/node/stream/default/Duplex/isPaused)(): boolean;

      The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

      ```
      const readable = new stream.Readable();

      readable.isPaused(); // === false
      readable.pause();
      readable.isPaused(); // === true
      readable.resume();
      readable.isPaused(); // === false
      ```
    - [iterator](https://bun.com/reference/node/stream/default/Duplex/iterator)(

      options?: { destroyOnReturn: boolean }

      ): AsyncIterator<any>;

      The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
    - [listenerCount](https://bun.com/reference/node/stream/default/Duplex/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/stream/default/Duplex/listeners)<K>(

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
    - [map](https://bun.com/reference/node/stream/default/Duplex/map)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

      @param fn

      a function to map over every chunk in the stream. Async or not.

      @returns

      a stream mapped with the function *fn*.
    - [off](https://bun.com/reference/node/stream/default/Duplex/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'close',

      listener: () => void

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

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'drain',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'end',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'finish',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'pause',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'readable',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'resume',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Duplex/on)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'close',

      listener: () => void

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

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'drain',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'end',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'finish',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'pause',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'readable',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'resume',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Duplex/once)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [pause](https://bun.com/reference/node/stream/default/Duplex/pause)(): this;

      The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

      ```
      const readable = getReadableStreamSomehow();
      readable.on('data', (chunk) => {
        console.log(`Received ${chunk.length} bytes of data.`);
        readable.pause();
        console.log('There will be no additional data for 1 second.');
        setTimeout(() => {
          console.log('Now data will start flowing again.');
          readable.resume();
        }, 1000);
      });
      ```

      The `readable.pause()` method has no effect if there is a `'readable'` event listener.
    - [pipe](https://bun.com/reference/node/stream/default/Duplex/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'close',

      listener: () => void

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

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Duplex/prependListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'close',

      listener: () => void

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

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Duplex/prependOnceListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [push](https://bun.com/reference/node/stream/default/Duplex/push)(

      chunk: any,

      encoding?: BufferEncoding

      ): boolean;
    - [rawListeners](https://bun.com/reference/node/stream/default/Duplex/rawListeners)<K>(

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
    - [read](https://bun.com/reference/node/stream/default/Duplex/read)(

      size?: number

      ): any;

      The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

      The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

      If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

      The `size` argument must be less than or equal to 1 GiB.

      The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

      ```
      const readable = getReadableStreamSomehow();

      // 'readable' may be triggered multiple times as data is buffered in
      readable.on('readable', () => {
        let chunk;
        console.log('Stream is readable (new data received in buffer)');
        // Use a loop to make sure we read all currently available data
        while (null !== (chunk = readable.read())) {
          console.log(`Read ${chunk.length} bytes of data...`);
        }
      });

      // 'end' will be triggered once when there is no more data available
      readable.on('end', () => {
        console.log('Reached end of stream.');
      });
      ```

      Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

      Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

      ```
      const chunks = [];

      readable.on('readable', () => {
        let chunk;
        while (null !== (chunk = readable.read())) {
          chunks.push(chunk);
        }
      });

      readable.on('end', () => {
        const content = chunks.join('');
      });
      ```

      A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

      If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

      Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

      @param size

      Optional argument to specify how much data to read.
    - [reduce](https://bun.com/reference/node/stream/default/Duplex/reduce)<T = any>(

      fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial?: undefined,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.

      [reduce](https://bun.com/reference/node/stream/default/Duplex/reduce)<T = any>(

      fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial: T,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.
    - [removeAllListeners](https://bun.com/reference/node/stream/default/Duplex/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'close',

      listener: () => void

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

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'end',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Duplex/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [resume](https://bun.com/reference/node/stream/default/Duplex/resume)(): this;

      The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

      The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

      ```
      getReadableStreamSomehow()
        .resume()
        .on('end', () => {
          console.log('Reached the end, but did not read anything.');
        });
      ```

      The `readable.resume()` method has no effect if there is a `'readable'` event listener.
    - [setDefaultEncoding](https://bun.com/reference/node/stream/default/Duplex/setDefaultEncoding)(

      encoding: BufferEncoding

      ): this;

      The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

      @param encoding

      The new default encoding
    - [setEncoding](https://bun.com/reference/node/stream/default/Duplex/setEncoding)(

      encoding: BufferEncoding

      ): this;

      The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

      By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

      The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

      ```
      const readable = getReadableStreamSomehow();
      readable.setEncoding('utf8');
      readable.on('data', (chunk) => {
        assert.equal(typeof chunk, 'string');
        console.log('Got %d characters of string data:', chunk.length);
      });
      ```

      @param encoding

      The encoding to use.
    - [setMaxListeners](https://bun.com/reference/node/stream/default/Duplex/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [some](https://bun.com/reference/node/stream/default/Duplex/some)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
    - [take](https://bun.com/reference/node/stream/default/Duplex/take)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks.

      @param limit

      the number of chunks to take from the readable.

      @returns

      a stream with *limit* chunks taken.
    - [toArray](https://bun.com/reference/node/stream/default/Duplex/toArray)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<any[]>;

      This method allows easily obtaining the contents of a stream.

      As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

      @returns

      a promise containing an array with the contents of the stream.
    - [uncork](https://bun.com/reference/node/stream/default/Duplex/uncork)(): void;

      The `writable.uncork()` method flushes all data buffered since cork was called.

      When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

      ```
      stream.cork();
      stream.write('some ');
      stream.write('data ');
      process.nextTick(() => stream.uncork());
      ```

      If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

      ```
      stream.cork();
      stream.write('some ');
      stream.cork();
      stream.write('data ');
      process.nextTick(() => {
        stream.uncork();
        // The data will not be flushed until uncork() is called a second time.
        stream.uncork();
      });
      ```

      See also: `writable.cork()`.
    - [unpipe](https://bun.com/reference/node/stream/default/Duplex/unpipe)(

      destination?: WritableStream

      ): this;

      The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

      If the `destination` is not specified, then *all* pipes are detached.

      If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

      ```
      import fs from 'node:fs';
      const readable = getReadableStreamSomehow();
      const writable = fs.createWriteStream('file.txt');
      // All the data from readable goes into 'file.txt',
      // but only for the first second.
      readable.pipe(writable);
      setTimeout(() => {
        console.log('Stop writing to file.txt.');
        readable.unpipe(writable);
        console.log('Manually close the file stream.');
        writable.end();
      }, 1000);
      ```

      @param destination

      Optional specific stream to unpipe
    - [unshift](https://bun.com/reference/node/stream/default/Duplex/unshift)(

      chunk: any,

      encoding?: BufferEncoding

      ): void;

      Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

      The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

      The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

      Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

      ```
      // Pull off a header delimited by \n\n.
      // Use unshift() if we get too much.
      // Call the callback with (error, header, stream).
      import { StringDecoder } from 'node:string_decoder';
      function parseHeader(stream, callback) {
        stream.on('error', callback);
        stream.on('readable', onReadable);
        const decoder = new StringDecoder('utf8');
        let header = '';
        function onReadable() {
          let chunk;
          while (null !== (chunk = stream.read())) {
            const str = decoder.write(chunk);
            if (str.includes('\n\n')) {
              // Found the header boundary.
              const split = str.split(/\n\n/);
              header += split.shift();
              const remaining = split.join('\n\n');
              const buf = Buffer.from(remaining, 'utf8');
              stream.removeListener('error', callback);
              // Remove the 'readable' listener before unshifting.
              stream.removeListener('readable', onReadable);
              if (buf.length)
                stream.unshift(buf);
              // Now the body of the message can be read from the stream.
              callback(null, header, stream);
              return;
            }
            // Still reading the header.
            header += str;
          }
        }
      }
      ```

      Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

      @param chunk

      Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

      @param encoding

      Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
    - [wrap](https://bun.com/reference/node/stream/default/Duplex/wrap)(

      stream: ReadableStream

      ): this;

      Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

      When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

      It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

      ```
      import { OldReader } from './old-api-module.js';
      import { Readable } from 'node:stream';
      const oreader = new OldReader();
      const myReader = new Readable().wrap(oreader);

      myReader.on('readable', () => {
        myReader.read(); // etc.
      });
      ```

      @param stream

      An "old style" readable stream
    - [write](https://bun.com/reference/node/stream/default/Duplex/write)(

      chunk: any,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

      [write](https://bun.com/reference/node/stream/default/Duplex/write)(

      chunk: any,

      encoding: BufferEncoding,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding, if `chunk` is a string.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
    - static [addAbortListener](https://bun.com/reference/node/stream/default/Duplex/addAbortListener)(

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
    - static [from](https://bun.com/reference/node/stream/default/Duplex/from)(

      src: string | Object | [Stream](https://bun.com/reference/node/stream/default) | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | [Blob](https://bun.com/reference/node/buffer/Blob) | Promise<any> | Iterable<any, any, any> | AsyncIterable<any, any, any> | AsyncGeneratorFunction

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating duplex streams.

      * `Stream` converts writable stream into writable `Duplex` and readable stream to `Duplex`.
      * `Blob` converts into readable `Duplex`.
      * `string` converts into readable `Duplex`.
      * `ArrayBuffer` converts into readable `Duplex`.
      * `AsyncIterable` converts into a readable `Duplex`. Cannot yield `null`.
      * `AsyncGeneratorFunction` converts into a readable/writable transform `Duplex`. Must take a source `AsyncIterable` as first parameter. Cannot yield `null`.
      * `AsyncFunction` converts into a writable `Duplex`. Must return either `null` or `undefined`
      * `Object ({ writable, readable })` converts `readable` and `writable` into `Stream` and then combines them into `Duplex` where the `Duplex` will write to the `writable` and read from the `readable`.
      * `Promise` converts into readable `Duplex`. Value `null` is ignored.
    - static [fromWeb](https://bun.com/reference/node/stream/default/Duplex/fromWeb)(

      duplexStream: { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) },

      options?: Pick<[DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>, 'signal' | 'allowHalfOpen' | 'decodeStrings' | 'encoding' | 'highWaterMark' | 'objectMode'>

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating a `Duplex` from a web `ReadableStream` and `WritableStream`.
    - static [getEventListeners](https://bun.com/reference/node/stream/default/Duplex/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/stream/default/Duplex/getMaxListeners)(

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
    - static [on](https://bun.com/reference/node/stream/default/Duplex/on)(

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

      static [on](https://bun.com/reference/node/stream/default/Duplex/on)(

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
    - static [once](https://bun.com/reference/node/stream/default/Duplex/once)(

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

      static [once](https://bun.com/reference/node/stream/default/Duplex/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/stream/default/Duplex/setMaxListeners)(

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
    - static [toWeb](https://bun.com/reference/node/stream/default/Duplex/toWeb)(

      streamDuplex: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

      ): { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) };

      A utility method for creating a web `ReadableStream` and `WritableStream` from a `Duplex`.
  + ### class [PassThrough](https://bun.com/reference/node/stream/default/PassThrough)

    The `stream.PassThrough` class is a trivial implementation of a `Transform` stream that simply passes the input bytes across to the output. Its purpose is primarily for examples and testing, but there are some use cases where `stream.PassThrough` is useful as a building block for novel sorts of streams.

    - [allowHalfOpen](https://bun.com/reference/node/stream/default/PassThrough/allowHalfOpen): boolean

      If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

      This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
    - readonly [closed](https://bun.com/reference/node/stream/default/PassThrough/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/stream/default/PassThrough/destroyed): boolean

      Is `true` after `readable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/stream/default/PassThrough/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - [readable](https://bun.com/reference/node/stream/default/PassThrough/readable): boolean

      Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
    - readonly [readableAborted](https://bun.com/reference/node/stream/default/PassThrough/readableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'end'`.
    - readonly [readableDidRead](https://bun.com/reference/node/stream/default/PassThrough/readableDidRead): boolean

      Returns whether `'data'` has been emitted.
    - readonly [readableEncoding](https://bun.com/reference/node/stream/default/PassThrough/readableEncoding): null | BufferEncoding

      Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
    - readonly [readableEnded](https://bun.com/reference/node/stream/default/PassThrough/readableEnded): boolean

      Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
    - readonly [readableFlowing](https://bun.com/reference/node/stream/default/PassThrough/readableFlowing): null | boolean

      This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
    - readonly [readableHighWaterMark](https://bun.com/reference/node/stream/default/PassThrough/readableHighWaterMark): number

      Returns the value of `highWaterMark` passed when creating this `Readable`.
    - readonly [readableLength](https://bun.com/reference/node/stream/default/PassThrough/readableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [readableObjectMode](https://bun.com/reference/node/stream/default/PassThrough/readableObjectMode): boolean

      Getter for the property `objectMode` of a given `Readable` stream.
    - readonly [writable](https://bun.com/reference/node/stream/default/PassThrough/writable): boolean

      Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
    - readonly [writableAborted](https://bun.com/reference/node/stream/default/PassThrough/writableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'finish'`.
    - readonly [writableCorked](https://bun.com/reference/node/stream/default/PassThrough/writableCorked): number

      Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
    - readonly [writableEnded](https://bun.com/reference/node/stream/default/PassThrough/writableEnded): boolean

      Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
    - readonly [writableFinished](https://bun.com/reference/node/stream/default/PassThrough/writableFinished): boolean

      Is set to `true` immediately before the `'finish'` event is emitted.
    - readonly [writableHighWaterMark](https://bun.com/reference/node/stream/default/PassThrough/writableHighWaterMark): number

      Return the value of `highWaterMark` passed when creating this `Writable`.
    - readonly [writableLength](https://bun.com/reference/node/stream/default/PassThrough/writableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [writableNeedDrain](https://bun.com/reference/node/stream/default/PassThrough/writableNeedDrain): boolean

      Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
    - readonly [writableObjectMode](https://bun.com/reference/node/stream/default/PassThrough/writableObjectMode): boolean

      Getter for the property `objectMode` of a given `Writable` stream.
    - static [captureRejections](https://bun.com/reference/node/stream/default/PassThrough/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/PassThrough/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/stream/default/PassThrough/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/stream/default/PassThrough/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [\_construct](https://bun.com/reference/node/stream/default/PassThrough/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/stream/default/PassThrough/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_final](https://bun.com/reference/node/stream/default/PassThrough/_final)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_flush](https://bun.com/reference/node/stream/default/PassThrough/_flush)(

      callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

      ): void;
    - [\_read](https://bun.com/reference/node/stream/default/PassThrough/_read)(

      size: number

      ): void;
    - [\_transform](https://bun.com/reference/node/stream/default/PassThrough/_transform)(

      chunk: any,

      encoding: BufferEncoding,

      callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

      ): void;
    - [\_write](https://bun.com/reference/node/stream/default/PassThrough/_write)(

      chunk: any,

      encoding: BufferEncoding,

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_writev](https://bun.com/reference/node/stream/default/PassThrough/_writev)(

      chunks: { chunk: any; encoding: BufferEncoding }[],

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/default/PassThrough/[asyncDispose])(): Promise<void>;

      Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/default/PassThrough/[asyncIterator])(): AsyncIterator<any>;

      @returns

      `AsyncIterator` to fully consume the stream.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/PassThrough/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'close',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'drain',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'end',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'finish',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'pause',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'readable',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'resume',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/PassThrough/addListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe
    - [asIndexedPairs](https://bun.com/reference/node/stream/default/PassThrough/asIndexedPairs)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

      @returns

      a stream of indexed pairs.
    - [compose](https://bun.com/reference/node/stream/default/PassThrough/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [cork](https://bun.com/reference/node/stream/default/PassThrough/cork)(): void;

      The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

      The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

      See also: `writable.uncork()`, `writable._writev()`.
    - [destroy](https://bun.com/reference/node/stream/default/PassThrough/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `readable._destroy()`.

      @param error

      Error which will be passed as payload in `'error'` event
    - [drop](https://bun.com/reference/node/stream/default/PassThrough/drop)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks dropped from the start.

      @param limit

      the number of chunks to drop from the readable.

      @returns

      a stream with *limit* chunks dropped from the start.
    - [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'close'

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

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'data',

      chunk: any

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'drain'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'end'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'error',

      err: [Error](https://bun.com/reference/globals/Error)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'finish'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'pause'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'pipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'readable'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'resume'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: 'unpipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/PassThrough/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [end](https://bun.com/reference/node/stream/default/PassThrough/end)(

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      [end](https://bun.com/reference/node/stream/default/PassThrough/end)(

      chunk: any,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      [end](https://bun.com/reference/node/stream/default/PassThrough/end)(

      chunk: any,

      encoding: BufferEncoding,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding if `chunk` is a string
    - [eventNames](https://bun.com/reference/node/stream/default/PassThrough/eventNames)(): string | symbol[];

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
    - [every](https://bun.com/reference/node/stream/default/PassThrough/every)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
    - [filter](https://bun.com/reference/node/stream/default/PassThrough/filter)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

      @param fn

      a function to filter chunks from the stream. Async or not.

      @returns

      a stream filtered with the predicate *fn*.
    - [find](https://bun.com/reference/node/stream/default/PassThrough/find)<T>(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<undefined | T>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

      [find](https://bun.com/reference/node/stream/default/PassThrough/find)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<any>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
    - [flatMap](https://bun.com/reference/node/stream/default/PassThrough/flatMap)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

      It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

      @param fn

      a function to map over every chunk in the stream. May be async. May be a stream or generator.

      @returns

      a stream flat-mapped with the function *fn*.
    - [forEach](https://bun.com/reference/node/stream/default/PassThrough/forEach)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<void>;

      This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

      This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

      This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise for when the stream has finished.
    - [getMaxListeners](https://bun.com/reference/node/stream/default/PassThrough/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [isPaused](https://bun.com/reference/node/stream/default/PassThrough/isPaused)(): boolean;

      The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

      ```
      const readable = new stream.Readable();

      readable.isPaused(); // === false
      readable.pause();
      readable.isPaused(); // === true
      readable.resume();
      readable.isPaused(); // === false
      ```
    - [iterator](https://bun.com/reference/node/stream/default/PassThrough/iterator)(

      options?: { destroyOnReturn: boolean }

      ): AsyncIterator<any>;

      The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
    - [listenerCount](https://bun.com/reference/node/stream/default/PassThrough/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/stream/default/PassThrough/listeners)<K>(

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
    - [map](https://bun.com/reference/node/stream/default/PassThrough/map)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

      @param fn

      a function to map over every chunk in the stream. Async or not.

      @returns

      a stream mapped with the function *fn*.
    - [off](https://bun.com/reference/node/stream/default/PassThrough/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'close',

      listener: () => void

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

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'drain',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'end',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'finish',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'pause',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'readable',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'resume',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'close',

      listener: () => void

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

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'drain',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'end',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'finish',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'pause',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'readable',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'resume',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [pause](https://bun.com/reference/node/stream/default/PassThrough/pause)(): this;

      The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

      ```
      const readable = getReadableStreamSomehow();
      readable.on('data', (chunk) => {
        console.log(`Received ${chunk.length} bytes of data.`);
        readable.pause();
        console.log('There will be no additional data for 1 second.');
        setTimeout(() => {
          console.log('Now data will start flowing again.');
          readable.resume();
        }, 1000);
      });
      ```

      The `readable.pause()` method has no effect if there is a `'readable'` event listener.
    - [pipe](https://bun.com/reference/node/stream/default/PassThrough/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'close',

      listener: () => void

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

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/PassThrough/prependListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'close',

      listener: () => void

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

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/PassThrough/prependOnceListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [push](https://bun.com/reference/node/stream/default/PassThrough/push)(

      chunk: any,

      encoding?: BufferEncoding

      ): boolean;
    - [rawListeners](https://bun.com/reference/node/stream/default/PassThrough/rawListeners)<K>(

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
    - [read](https://bun.com/reference/node/stream/default/PassThrough/read)(

      size?: number

      ): any;

      The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

      The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

      If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

      The `size` argument must be less than or equal to 1 GiB.

      The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

      ```
      const readable = getReadableStreamSomehow();

      // 'readable' may be triggered multiple times as data is buffered in
      readable.on('readable', () => {
        let chunk;
        console.log('Stream is readable (new data received in buffer)');
        // Use a loop to make sure we read all currently available data
        while (null !== (chunk = readable.read())) {
          console.log(`Read ${chunk.length} bytes of data...`);
        }
      });

      // 'end' will be triggered once when there is no more data available
      readable.on('end', () => {
        console.log('Reached end of stream.');
      });
      ```

      Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

      Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

      ```
      const chunks = [];

      readable.on('readable', () => {
        let chunk;
        while (null !== (chunk = readable.read())) {
          chunks.push(chunk);
        }
      });

      readable.on('end', () => {
        const content = chunks.join('');
      });
      ```

      A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

      If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

      Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

      @param size

      Optional argument to specify how much data to read.
    - [reduce](https://bun.com/reference/node/stream/default/PassThrough/reduce)<T = any>(

      fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial?: undefined,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.

      [reduce](https://bun.com/reference/node/stream/default/PassThrough/reduce)<T = any>(

      fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial: T,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.
    - [removeAllListeners](https://bun.com/reference/node/stream/default/PassThrough/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'close',

      listener: () => void

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

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'end',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/PassThrough/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [resume](https://bun.com/reference/node/stream/default/PassThrough/resume)(): this;

      The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

      The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

      ```
      getReadableStreamSomehow()
        .resume()
        .on('end', () => {
          console.log('Reached the end, but did not read anything.');
        });
      ```

      The `readable.resume()` method has no effect if there is a `'readable'` event listener.
    - [setDefaultEncoding](https://bun.com/reference/node/stream/default/PassThrough/setDefaultEncoding)(

      encoding: BufferEncoding

      ): this;

      The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

      @param encoding

      The new default encoding
    - [setEncoding](https://bun.com/reference/node/stream/default/PassThrough/setEncoding)(

      encoding: BufferEncoding

      ): this;

      The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

      By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

      The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

      ```
      const readable = getReadableStreamSomehow();
      readable.setEncoding('utf8');
      readable.on('data', (chunk) => {
        assert.equal(typeof chunk, 'string');
        console.log('Got %d characters of string data:', chunk.length);
      });
      ```

      @param encoding

      The encoding to use.
    - [setMaxListeners](https://bun.com/reference/node/stream/default/PassThrough/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [some](https://bun.com/reference/node/stream/default/PassThrough/some)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
    - [take](https://bun.com/reference/node/stream/default/PassThrough/take)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks.

      @param limit

      the number of chunks to take from the readable.

      @returns

      a stream with *limit* chunks taken.
    - [toArray](https://bun.com/reference/node/stream/default/PassThrough/toArray)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<any[]>;

      This method allows easily obtaining the contents of a stream.

      As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

      @returns

      a promise containing an array with the contents of the stream.
    - [uncork](https://bun.com/reference/node/stream/default/PassThrough/uncork)(): void;

      The `writable.uncork()` method flushes all data buffered since cork was called.

      When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

      ```
      stream.cork();
      stream.write('some ');
      stream.write('data ');
      process.nextTick(() => stream.uncork());
      ```

      If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

      ```
      stream.cork();
      stream.write('some ');
      stream.cork();
      stream.write('data ');
      process.nextTick(() => {
        stream.uncork();
        // The data will not be flushed until uncork() is called a second time.
        stream.uncork();
      });
      ```

      See also: `writable.cork()`.
    - [unpipe](https://bun.com/reference/node/stream/default/PassThrough/unpipe)(

      destination?: WritableStream

      ): this;

      The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

      If the `destination` is not specified, then *all* pipes are detached.

      If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

      ```
      import fs from 'node:fs';
      const readable = getReadableStreamSomehow();
      const writable = fs.createWriteStream('file.txt');
      // All the data from readable goes into 'file.txt',
      // but only for the first second.
      readable.pipe(writable);
      setTimeout(() => {
        console.log('Stop writing to file.txt.');
        readable.unpipe(writable);
        console.log('Manually close the file stream.');
        writable.end();
      }, 1000);
      ```

      @param destination

      Optional specific stream to unpipe
    - [unshift](https://bun.com/reference/node/stream/default/PassThrough/unshift)(

      chunk: any,

      encoding?: BufferEncoding

      ): void;

      Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

      The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

      The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

      Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

      ```
      // Pull off a header delimited by \n\n.
      // Use unshift() if we get too much.
      // Call the callback with (error, header, stream).
      import { StringDecoder } from 'node:string_decoder';
      function parseHeader(stream, callback) {
        stream.on('error', callback);
        stream.on('readable', onReadable);
        const decoder = new StringDecoder('utf8');
        let header = '';
        function onReadable() {
          let chunk;
          while (null !== (chunk = stream.read())) {
            const str = decoder.write(chunk);
            if (str.includes('\n\n')) {
              // Found the header boundary.
              const split = str.split(/\n\n/);
              header += split.shift();
              const remaining = split.join('\n\n');
              const buf = Buffer.from(remaining, 'utf8');
              stream.removeListener('error', callback);
              // Remove the 'readable' listener before unshifting.
              stream.removeListener('readable', onReadable);
              if (buf.length)
                stream.unshift(buf);
              // Now the body of the message can be read from the stream.
              callback(null, header, stream);
              return;
            }
            // Still reading the header.
            header += str;
          }
        }
      }
      ```

      Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

      @param chunk

      Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

      @param encoding

      Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
    - [wrap](https://bun.com/reference/node/stream/default/PassThrough/wrap)(

      stream: ReadableStream

      ): this;

      Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

      When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

      It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

      ```
      import { OldReader } from './old-api-module.js';
      import { Readable } from 'node:stream';
      const oreader = new OldReader();
      const myReader = new Readable().wrap(oreader);

      myReader.on('readable', () => {
        myReader.read(); // etc.
      });
      ```

      @param stream

      An "old style" readable stream
    - [write](https://bun.com/reference/node/stream/default/PassThrough/write)(

      chunk: any,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

      [write](https://bun.com/reference/node/stream/default/PassThrough/write)(

      chunk: any,

      encoding: BufferEncoding,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding, if `chunk` is a string.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
    - static [addAbortListener](https://bun.com/reference/node/stream/default/PassThrough/addAbortListener)(

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
    - static [from](https://bun.com/reference/node/stream/default/PassThrough/from)(

      src: string | Object | [Stream](https://bun.com/reference/node/stream/default) | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | [Blob](https://bun.com/reference/node/buffer/Blob) | Promise<any> | Iterable<any, any, any> | AsyncIterable<any, any, any> | AsyncGeneratorFunction

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating duplex streams.

      * `Stream` converts writable stream into writable `Duplex` and readable stream to `Duplex`.
      * `Blob` converts into readable `Duplex`.
      * `string` converts into readable `Duplex`.
      * `ArrayBuffer` converts into readable `Duplex`.
      * `AsyncIterable` converts into a readable `Duplex`. Cannot yield `null`.
      * `AsyncGeneratorFunction` converts into a readable/writable transform `Duplex`. Must take a source `AsyncIterable` as first parameter. Cannot yield `null`.
      * `AsyncFunction` converts into a writable `Duplex`. Must return either `null` or `undefined`
      * `Object ({ writable, readable })` converts `readable` and `writable` into `Stream` and then combines them into `Duplex` where the `Duplex` will write to the `writable` and read from the `readable`.
      * `Promise` converts into readable `Duplex`. Value `null` is ignored.
    - static [fromWeb](https://bun.com/reference/node/stream/default/PassThrough/fromWeb)(

      duplexStream: { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) },

      options?: Pick<[DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>, 'signal' | 'allowHalfOpen' | 'decodeStrings' | 'encoding' | 'highWaterMark' | 'objectMode'>

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating a `Duplex` from a web `ReadableStream` and `WritableStream`.
    - static [getEventListeners](https://bun.com/reference/node/stream/default/PassThrough/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/stream/default/PassThrough/getMaxListeners)(

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
    - static [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

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

      static [on](https://bun.com/reference/node/stream/default/PassThrough/on)(

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
    - static [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

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

      static [once](https://bun.com/reference/node/stream/default/PassThrough/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/stream/default/PassThrough/setMaxListeners)(

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
    - static [toWeb](https://bun.com/reference/node/stream/default/PassThrough/toWeb)(

      streamDuplex: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

      ): { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) };

      A utility method for creating a web `ReadableStream` and `WritableStream` from a `Duplex`.
  + ### class [Readable](https://bun.com/reference/node/stream/default/Readable)

    - readonly [closed](https://bun.com/reference/node/stream/default/Readable/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/stream/default/Readable/destroyed): boolean

      Is `true` after `readable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/stream/default/Readable/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - [readable](https://bun.com/reference/node/stream/default/Readable/readable): boolean

      Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
    - readonly [readableAborted](https://bun.com/reference/node/stream/default/Readable/readableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'end'`.
    - readonly [readableDidRead](https://bun.com/reference/node/stream/default/Readable/readableDidRead): boolean

      Returns whether `'data'` has been emitted.
    - readonly [readableEncoding](https://bun.com/reference/node/stream/default/Readable/readableEncoding): null | BufferEncoding

      Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
    - readonly [readableEnded](https://bun.com/reference/node/stream/default/Readable/readableEnded): boolean

      Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
    - readonly [readableFlowing](https://bun.com/reference/node/stream/default/Readable/readableFlowing): null | boolean

      This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
    - readonly [readableHighWaterMark](https://bun.com/reference/node/stream/default/Readable/readableHighWaterMark): number

      Returns the value of `highWaterMark` passed when creating this `Readable`.
    - readonly [readableLength](https://bun.com/reference/node/stream/default/Readable/readableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [readableObjectMode](https://bun.com/reference/node/stream/default/Readable/readableObjectMode): boolean

      Getter for the property `objectMode` of a given `Readable` stream.
    - static [captureRejections](https://bun.com/reference/node/stream/default/Readable/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/Readable/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/stream/default/Readable/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/stream/default/Readable/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [\_construct](https://bun.com/reference/node/stream/default/Readable/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/stream/default/Readable/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_read](https://bun.com/reference/node/stream/default/Readable/_read)(

      size: number

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/default/Readable/[asyncDispose])(): Promise<void>;

      Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/default/Readable/[asyncIterator])(): AsyncIterator<any>;

      @returns

      `AsyncIterator` to fully consume the stream.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/Readable/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'close',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'end',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'pause',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'readable',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: 'resume',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/stream/default/Readable/addListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume
    - [asIndexedPairs](https://bun.com/reference/node/stream/default/Readable/asIndexedPairs)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

      @returns

      a stream of indexed pairs.
    - [compose](https://bun.com/reference/node/stream/default/Readable/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [destroy](https://bun.com/reference/node/stream/default/Readable/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `readable._destroy()`.

      @param error

      Error which will be passed as payload in `'error'` event
    - [drop](https://bun.com/reference/node/stream/default/Readable/drop)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks dropped from the start.

      @param limit

      the number of chunks to drop from the readable.

      @returns

      a stream with *limit* chunks dropped from the start.
    - [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'close'

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

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'data',

      chunk: any

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'end'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'error',

      err: [Error](https://bun.com/reference/globals/Error)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'pause'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'readable'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: 'resume'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Readable/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [eventNames](https://bun.com/reference/node/stream/default/Readable/eventNames)(): string | symbol[];

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
    - [every](https://bun.com/reference/node/stream/default/Readable/every)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
    - [filter](https://bun.com/reference/node/stream/default/Readable/filter)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

      @param fn

      a function to filter chunks from the stream. Async or not.

      @returns

      a stream filtered with the predicate *fn*.
    - [find](https://bun.com/reference/node/stream/default/Readable/find)<T>(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<undefined | T>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

      [find](https://bun.com/reference/node/stream/default/Readable/find)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<any>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
    - [flatMap](https://bun.com/reference/node/stream/default/Readable/flatMap)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

      It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

      @param fn

      a function to map over every chunk in the stream. May be async. May be a stream or generator.

      @returns

      a stream flat-mapped with the function *fn*.
    - [forEach](https://bun.com/reference/node/stream/default/Readable/forEach)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<void>;

      This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

      This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

      This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise for when the stream has finished.
    - [getMaxListeners](https://bun.com/reference/node/stream/default/Readable/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [isPaused](https://bun.com/reference/node/stream/default/Readable/isPaused)(): boolean;

      The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

      ```
      const readable = new stream.Readable();

      readable.isPaused(); // === false
      readable.pause();
      readable.isPaused(); // === true
      readable.resume();
      readable.isPaused(); // === false
      ```
    - [iterator](https://bun.com/reference/node/stream/default/Readable/iterator)(

      options?: { destroyOnReturn: boolean }

      ): AsyncIterator<any>;

      The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
    - [listenerCount](https://bun.com/reference/node/stream/default/Readable/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/stream/default/Readable/listeners)<K>(

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
    - [map](https://bun.com/reference/node/stream/default/Readable/map)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

      @param fn

      a function to map over every chunk in the stream. Async or not.

      @returns

      a stream mapped with the function *fn*.
    - [off](https://bun.com/reference/node/stream/default/Readable/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'close',

      listener: () => void

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

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'end',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'pause',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'readable',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: 'resume',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Readable/on)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'close',

      listener: () => void

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

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'end',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'pause',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'readable',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: 'resume',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Readable/once)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [pause](https://bun.com/reference/node/stream/default/Readable/pause)(): this;

      The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

      ```
      const readable = getReadableStreamSomehow();
      readable.on('data', (chunk) => {
        console.log(`Received ${chunk.length} bytes of data.`);
        readable.pause();
        console.log('There will be no additional data for 1 second.');
        setTimeout(() => {
          console.log('Now data will start flowing again.');
          readable.resume();
        }, 1000);
      });
      ```

      The `readable.pause()` method has no effect if there is a `'readable'` event listener.
    - [pipe](https://bun.com/reference/node/stream/default/Readable/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'close',

      listener: () => void

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

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Readable/prependListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'close',

      listener: () => void

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

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Readable/prependOnceListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [push](https://bun.com/reference/node/stream/default/Readable/push)(

      chunk: any,

      encoding?: BufferEncoding

      ): boolean;
    - [rawListeners](https://bun.com/reference/node/stream/default/Readable/rawListeners)<K>(

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
    - [read](https://bun.com/reference/node/stream/default/Readable/read)(

      size?: number

      ): any;

      The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

      The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

      If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

      The `size` argument must be less than or equal to 1 GiB.

      The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

      ```
      const readable = getReadableStreamSomehow();

      // 'readable' may be triggered multiple times as data is buffered in
      readable.on('readable', () => {
        let chunk;
        console.log('Stream is readable (new data received in buffer)');
        // Use a loop to make sure we read all currently available data
        while (null !== (chunk = readable.read())) {
          console.log(`Read ${chunk.length} bytes of data...`);
        }
      });

      // 'end' will be triggered once when there is no more data available
      readable.on('end', () => {
        console.log('Reached end of stream.');
      });
      ```

      Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

      Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

      ```
      const chunks = [];

      readable.on('readable', () => {
        let chunk;
        while (null !== (chunk = readable.read())) {
          chunks.push(chunk);
        }
      });

      readable.on('end', () => {
        const content = chunks.join('');
      });
      ```

      A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

      If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

      Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

      @param size

      Optional argument to specify how much data to read.
    - [reduce](https://bun.com/reference/node/stream/default/Readable/reduce)<T = any>(

      fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial?: undefined,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.

      [reduce](https://bun.com/reference/node/stream/default/Readable/reduce)<T = any>(

      fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial: T,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.
    - [removeAllListeners](https://bun.com/reference/node/stream/default/Readable/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'close',

      listener: () => void

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

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'end',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Readable/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [resume](https://bun.com/reference/node/stream/default/Readable/resume)(): this;

      The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

      The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

      ```
      getReadableStreamSomehow()
        .resume()
        .on('end', () => {
          console.log('Reached the end, but did not read anything.');
        });
      ```

      The `readable.resume()` method has no effect if there is a `'readable'` event listener.
    - [setEncoding](https://bun.com/reference/node/stream/default/Readable/setEncoding)(

      encoding: BufferEncoding

      ): this;

      The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

      By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

      The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

      ```
      const readable = getReadableStreamSomehow();
      readable.setEncoding('utf8');
      readable.on('data', (chunk) => {
        assert.equal(typeof chunk, 'string');
        console.log('Got %d characters of string data:', chunk.length);
      });
      ```

      @param encoding

      The encoding to use.
    - [setMaxListeners](https://bun.com/reference/node/stream/default/Readable/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [some](https://bun.com/reference/node/stream/default/Readable/some)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
    - [take](https://bun.com/reference/node/stream/default/Readable/take)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks.

      @param limit

      the number of chunks to take from the readable.

      @returns

      a stream with *limit* chunks taken.
    - [toArray](https://bun.com/reference/node/stream/default/Readable/toArray)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<any[]>;

      This method allows easily obtaining the contents of a stream.

      As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

      @returns

      a promise containing an array with the contents of the stream.
    - [unpipe](https://bun.com/reference/node/stream/default/Readable/unpipe)(

      destination?: WritableStream

      ): this;

      The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

      If the `destination` is not specified, then *all* pipes are detached.

      If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

      ```
      import fs from 'node:fs';
      const readable = getReadableStreamSomehow();
      const writable = fs.createWriteStream('file.txt');
      // All the data from readable goes into 'file.txt',
      // but only for the first second.
      readable.pipe(writable);
      setTimeout(() => {
        console.log('Stop writing to file.txt.');
        readable.unpipe(writable);
        console.log('Manually close the file stream.');
        writable.end();
      }, 1000);
      ```

      @param destination

      Optional specific stream to unpipe
    - [unshift](https://bun.com/reference/node/stream/default/Readable/unshift)(

      chunk: any,

      encoding?: BufferEncoding

      ): void;

      Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

      The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

      The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

      Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

      ```
      // Pull off a header delimited by \n\n.
      // Use unshift() if we get too much.
      // Call the callback with (error, header, stream).
      import { StringDecoder } from 'node:string_decoder';
      function parseHeader(stream, callback) {
        stream.on('error', callback);
        stream.on('readable', onReadable);
        const decoder = new StringDecoder('utf8');
        let header = '';
        function onReadable() {
          let chunk;
          while (null !== (chunk = stream.read())) {
            const str = decoder.write(chunk);
            if (str.includes('\n\n')) {
              // Found the header boundary.
              const split = str.split(/\n\n/);
              header += split.shift();
              const remaining = split.join('\n\n');
              const buf = Buffer.from(remaining, 'utf8');
              stream.removeListener('error', callback);
              // Remove the 'readable' listener before unshifting.
              stream.removeListener('readable', onReadable);
              if (buf.length)
                stream.unshift(buf);
              // Now the body of the message can be read from the stream.
              callback(null, header, stream);
              return;
            }
            // Still reading the header.
            header += str;
          }
        }
      }
      ```

      Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

      @param chunk

      Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

      @param encoding

      Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
    - [wrap](https://bun.com/reference/node/stream/default/Readable/wrap)(

      stream: ReadableStream

      ): this;

      Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

      When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

      It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

      ```
      import { OldReader } from './old-api-module.js';
      import { Readable } from 'node:stream';
      const oreader = new OldReader();
      const myReader = new Readable().wrap(oreader);

      myReader.on('readable', () => {
        myReader.read(); // etc.
      });
      ```

      @param stream

      An "old style" readable stream
    - static [addAbortListener](https://bun.com/reference/node/stream/default/Readable/addAbortListener)(

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
    - static [from](https://bun.com/reference/node/stream/default/Readable/from)(

      iterable: Iterable<any, any, any> | AsyncIterable<any, any, any>,

      options?: [ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      A utility method for creating Readable Streams out of iterators.

      @param iterable

      Object implementing the `Symbol.asyncIterator` or `Symbol.iterator` iterable protocol. Emits an 'error' event if a null value is passed.

      @param options

      Options provided to `new stream.Readable([options])`. By default, `Readable.from()` will set `options.objectMode` to `true`, unless this is explicitly opted out by setting `options.objectMode` to `false`.
    - static [fromWeb](https://bun.com/reference/node/stream/default/Readable/fromWeb)(

      readableStream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream),

      options?: Pick<[ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>, 'signal' | 'encoding' | 'highWaterMark' | 'objectMode'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      A utility method for creating a `Readable` from a web `ReadableStream`.
    - static [getEventListeners](https://bun.com/reference/node/stream/default/Readable/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/stream/default/Readable/getMaxListeners)(

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
    - static [isDisturbed](https://bun.com/reference/node/stream/default/Readable/isDisturbed)(

      stream: [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream

      ): boolean;

      Returns whether the stream has been read from or cancelled.
    - static [on](https://bun.com/reference/node/stream/default/Readable/on)(

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

      static [on](https://bun.com/reference/node/stream/default/Readable/on)(

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
    - static [once](https://bun.com/reference/node/stream/default/Readable/once)(

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

      static [once](https://bun.com/reference/node/stream/default/Readable/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/stream/default/Readable/setMaxListeners)(

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
    - static [toWeb](https://bun.com/reference/node/stream/default/Readable/toWeb)(

      streamReadable: [Readable](https://bun.com/reference/node/stream/default/Readable),

      options?: { strategy: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<any> }

      ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

      A utility method for creating a web `ReadableStream` from a `Readable`.
  + ### class [Transform](https://bun.com/reference/node/stream/default/Transform)

    Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

    Examples of `Transform` streams include:

    - `zlib streams`
    - `crypto streams`

    - [allowHalfOpen](https://bun.com/reference/node/stream/default/Transform/allowHalfOpen): boolean

      If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

      This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
    - readonly [closed](https://bun.com/reference/node/stream/default/Transform/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/stream/default/Transform/destroyed): boolean

      Is `true` after `readable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/stream/default/Transform/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - [readable](https://bun.com/reference/node/stream/default/Transform/readable): boolean

      Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
    - readonly [readableAborted](https://bun.com/reference/node/stream/default/Transform/readableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'end'`.
    - readonly [readableDidRead](https://bun.com/reference/node/stream/default/Transform/readableDidRead): boolean

      Returns whether `'data'` has been emitted.
    - readonly [readableEncoding](https://bun.com/reference/node/stream/default/Transform/readableEncoding): null | BufferEncoding

      Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
    - readonly [readableEnded](https://bun.com/reference/node/stream/default/Transform/readableEnded): boolean

      Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
    - readonly [readableFlowing](https://bun.com/reference/node/stream/default/Transform/readableFlowing): null | boolean

      This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
    - readonly [readableHighWaterMark](https://bun.com/reference/node/stream/default/Transform/readableHighWaterMark): number

      Returns the value of `highWaterMark` passed when creating this `Readable`.
    - readonly [readableLength](https://bun.com/reference/node/stream/default/Transform/readableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [readableObjectMode](https://bun.com/reference/node/stream/default/Transform/readableObjectMode): boolean

      Getter for the property `objectMode` of a given `Readable` stream.
    - readonly [writable](https://bun.com/reference/node/stream/default/Transform/writable): boolean

      Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
    - readonly [writableAborted](https://bun.com/reference/node/stream/default/Transform/writableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'finish'`.
    - readonly [writableCorked](https://bun.com/reference/node/stream/default/Transform/writableCorked): number

      Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
    - readonly [writableEnded](https://bun.com/reference/node/stream/default/Transform/writableEnded): boolean

      Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
    - readonly [writableFinished](https://bun.com/reference/node/stream/default/Transform/writableFinished): boolean

      Is set to `true` immediately before the `'finish'` event is emitted.
    - readonly [writableHighWaterMark](https://bun.com/reference/node/stream/default/Transform/writableHighWaterMark): number

      Return the value of `highWaterMark` passed when creating this `Writable`.
    - readonly [writableLength](https://bun.com/reference/node/stream/default/Transform/writableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [writableNeedDrain](https://bun.com/reference/node/stream/default/Transform/writableNeedDrain): boolean

      Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
    - readonly [writableObjectMode](https://bun.com/reference/node/stream/default/Transform/writableObjectMode): boolean

      Getter for the property `objectMode` of a given `Writable` stream.
    - static [captureRejections](https://bun.com/reference/node/stream/default/Transform/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/Transform/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/stream/default/Transform/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/stream/default/Transform/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [\_construct](https://bun.com/reference/node/stream/default/Transform/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/stream/default/Transform/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_final](https://bun.com/reference/node/stream/default/Transform/_final)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_flush](https://bun.com/reference/node/stream/default/Transform/_flush)(

      callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

      ): void;
    - [\_read](https://bun.com/reference/node/stream/default/Transform/_read)(

      size: number

      ): void;
    - [\_transform](https://bun.com/reference/node/stream/default/Transform/_transform)(

      chunk: any,

      encoding: BufferEncoding,

      callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

      ): void;
    - [\_write](https://bun.com/reference/node/stream/default/Transform/_write)(

      chunk: any,

      encoding: BufferEncoding,

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_writev](https://bun.com/reference/node/stream/default/Transform/_writev)(

      chunks: { chunk: any; encoding: BufferEncoding }[],

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/default/Transform/[asyncDispose])(): Promise<void>;

      Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/default/Transform/[asyncIterator])(): AsyncIterator<any>;

      @returns

      `AsyncIterator` to fully consume the stream.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/Transform/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'close',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'drain',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'end',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'finish',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'pause',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'readable',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'resume',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Transform/addListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. drain
      4. end
      5. error
      6. finish
      7. pause
      8. pipe
      9. readable
      10. resume
      11. unpipe
    - [asIndexedPairs](https://bun.com/reference/node/stream/default/Transform/asIndexedPairs)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

      @returns

      a stream of indexed pairs.
    - [compose](https://bun.com/reference/node/stream/default/Transform/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [cork](https://bun.com/reference/node/stream/default/Transform/cork)(): void;

      The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

      The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

      See also: `writable.uncork()`, `writable._writev()`.
    - [destroy](https://bun.com/reference/node/stream/default/Transform/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `readable._destroy()`.

      @param error

      Error which will be passed as payload in `'error'` event
    - [drop](https://bun.com/reference/node/stream/default/Transform/drop)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks dropped from the start.

      @param limit

      the number of chunks to drop from the readable.

      @returns

      a stream with *limit* chunks dropped from the start.
    - [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'close'

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

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'data',

      chunk: any

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'drain'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'end'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'error',

      err: [Error](https://bun.com/reference/globals/Error)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'finish'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'pause'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'pipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'readable'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'resume'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: 'unpipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Transform/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [end](https://bun.com/reference/node/stream/default/Transform/end)(

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      [end](https://bun.com/reference/node/stream/default/Transform/end)(

      chunk: any,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      [end](https://bun.com/reference/node/stream/default/Transform/end)(

      chunk: any,

      encoding: BufferEncoding,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding if `chunk` is a string
    - [eventNames](https://bun.com/reference/node/stream/default/Transform/eventNames)(): string | symbol[];

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
    - [every](https://bun.com/reference/node/stream/default/Transform/every)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
    - [filter](https://bun.com/reference/node/stream/default/Transform/filter)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

      @param fn

      a function to filter chunks from the stream. Async or not.

      @returns

      a stream filtered with the predicate *fn*.
    - [find](https://bun.com/reference/node/stream/default/Transform/find)<T>(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<undefined | T>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

      [find](https://bun.com/reference/node/stream/default/Transform/find)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<any>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
    - [flatMap](https://bun.com/reference/node/stream/default/Transform/flatMap)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

      It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

      @param fn

      a function to map over every chunk in the stream. May be async. May be a stream or generator.

      @returns

      a stream flat-mapped with the function *fn*.
    - [forEach](https://bun.com/reference/node/stream/default/Transform/forEach)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<void>;

      This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

      This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

      This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise for when the stream has finished.
    - [getMaxListeners](https://bun.com/reference/node/stream/default/Transform/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [isPaused](https://bun.com/reference/node/stream/default/Transform/isPaused)(): boolean;

      The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

      ```
      const readable = new stream.Readable();

      readable.isPaused(); // === false
      readable.pause();
      readable.isPaused(); // === true
      readable.resume();
      readable.isPaused(); // === false
      ```
    - [iterator](https://bun.com/reference/node/stream/default/Transform/iterator)(

      options?: { destroyOnReturn: boolean }

      ): AsyncIterator<any>;

      The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
    - [listenerCount](https://bun.com/reference/node/stream/default/Transform/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/stream/default/Transform/listeners)<K>(

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
    - [map](https://bun.com/reference/node/stream/default/Transform/map)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

      @param fn

      a function to map over every chunk in the stream. Async or not.

      @returns

      a stream mapped with the function *fn*.
    - [off](https://bun.com/reference/node/stream/default/Transform/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'close',

      listener: () => void

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

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'drain',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'end',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'finish',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'pause',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'readable',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'resume',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Transform/on)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'close',

      listener: () => void

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

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'drain',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'end',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'finish',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'pause',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'readable',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'resume',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Transform/once)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [pause](https://bun.com/reference/node/stream/default/Transform/pause)(): this;

      The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

      ```
      const readable = getReadableStreamSomehow();
      readable.on('data', (chunk) => {
        console.log(`Received ${chunk.length} bytes of data.`);
        readable.pause();
        console.log('There will be no additional data for 1 second.');
        setTimeout(() => {
          console.log('Now data will start flowing again.');
          readable.resume();
        }, 1000);
      });
      ```

      The `readable.pause()` method has no effect if there is a `'readable'` event listener.
    - [pipe](https://bun.com/reference/node/stream/default/Transform/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'close',

      listener: () => void

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

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Transform/prependListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'close',

      listener: () => void

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

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'end',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Transform/prependOnceListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [push](https://bun.com/reference/node/stream/default/Transform/push)(

      chunk: any,

      encoding?: BufferEncoding

      ): boolean;
    - [rawListeners](https://bun.com/reference/node/stream/default/Transform/rawListeners)<K>(

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
    - [read](https://bun.com/reference/node/stream/default/Transform/read)(

      size?: number

      ): any;

      The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

      The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

      If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

      The `size` argument must be less than or equal to 1 GiB.

      The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

      ```
      const readable = getReadableStreamSomehow();

      // 'readable' may be triggered multiple times as data is buffered in
      readable.on('readable', () => {
        let chunk;
        console.log('Stream is readable (new data received in buffer)');
        // Use a loop to make sure we read all currently available data
        while (null !== (chunk = readable.read())) {
          console.log(`Read ${chunk.length} bytes of data...`);
        }
      });

      // 'end' will be triggered once when there is no more data available
      readable.on('end', () => {
        console.log('Reached end of stream.');
      });
      ```

      Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

      Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

      ```
      const chunks = [];

      readable.on('readable', () => {
        let chunk;
        while (null !== (chunk = readable.read())) {
          chunks.push(chunk);
        }
      });

      readable.on('end', () => {
        const content = chunks.join('');
      });
      ```

      A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

      If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

      Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

      @param size

      Optional argument to specify how much data to read.
    - [reduce](https://bun.com/reference/node/stream/default/Transform/reduce)<T = any>(

      fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial?: undefined,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.

      [reduce](https://bun.com/reference/node/stream/default/Transform/reduce)<T = any>(

      fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial: T,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.
    - [removeAllListeners](https://bun.com/reference/node/stream/default/Transform/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'close',

      listener: () => void

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

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'end',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Transform/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [resume](https://bun.com/reference/node/stream/default/Transform/resume)(): this;

      The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

      The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

      ```
      getReadableStreamSomehow()
        .resume()
        .on('end', () => {
          console.log('Reached the end, but did not read anything.');
        });
      ```

      The `readable.resume()` method has no effect if there is a `'readable'` event listener.
    - [setDefaultEncoding](https://bun.com/reference/node/stream/default/Transform/setDefaultEncoding)(

      encoding: BufferEncoding

      ): this;

      The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

      @param encoding

      The new default encoding
    - [setEncoding](https://bun.com/reference/node/stream/default/Transform/setEncoding)(

      encoding: BufferEncoding

      ): this;

      The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

      By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

      The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

      ```
      const readable = getReadableStreamSomehow();
      readable.setEncoding('utf8');
      readable.on('data', (chunk) => {
        assert.equal(typeof chunk, 'string');
        console.log('Got %d characters of string data:', chunk.length);
      });
      ```

      @param encoding

      The encoding to use.
    - [setMaxListeners](https://bun.com/reference/node/stream/default/Transform/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [some](https://bun.com/reference/node/stream/default/Transform/some)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
    - [take](https://bun.com/reference/node/stream/default/Transform/take)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks.

      @param limit

      the number of chunks to take from the readable.

      @returns

      a stream with *limit* chunks taken.
    - [toArray](https://bun.com/reference/node/stream/default/Transform/toArray)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<any[]>;

      This method allows easily obtaining the contents of a stream.

      As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

      @returns

      a promise containing an array with the contents of the stream.
    - [uncork](https://bun.com/reference/node/stream/default/Transform/uncork)(): void;

      The `writable.uncork()` method flushes all data buffered since cork was called.

      When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

      ```
      stream.cork();
      stream.write('some ');
      stream.write('data ');
      process.nextTick(() => stream.uncork());
      ```

      If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

      ```
      stream.cork();
      stream.write('some ');
      stream.cork();
      stream.write('data ');
      process.nextTick(() => {
        stream.uncork();
        // The data will not be flushed until uncork() is called a second time.
        stream.uncork();
      });
      ```

      See also: `writable.cork()`.
    - [unpipe](https://bun.com/reference/node/stream/default/Transform/unpipe)(

      destination?: WritableStream

      ): this;

      The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

      If the `destination` is not specified, then *all* pipes are detached.

      If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

      ```
      import fs from 'node:fs';
      const readable = getReadableStreamSomehow();
      const writable = fs.createWriteStream('file.txt');
      // All the data from readable goes into 'file.txt',
      // but only for the first second.
      readable.pipe(writable);
      setTimeout(() => {
        console.log('Stop writing to file.txt.');
        readable.unpipe(writable);
        console.log('Manually close the file stream.');
        writable.end();
      }, 1000);
      ```

      @param destination

      Optional specific stream to unpipe
    - [unshift](https://bun.com/reference/node/stream/default/Transform/unshift)(

      chunk: any,

      encoding?: BufferEncoding

      ): void;

      Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

      The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

      The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

      Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

      ```
      // Pull off a header delimited by \n\n.
      // Use unshift() if we get too much.
      // Call the callback with (error, header, stream).
      import { StringDecoder } from 'node:string_decoder';
      function parseHeader(stream, callback) {
        stream.on('error', callback);
        stream.on('readable', onReadable);
        const decoder = new StringDecoder('utf8');
        let header = '';
        function onReadable() {
          let chunk;
          while (null !== (chunk = stream.read())) {
            const str = decoder.write(chunk);
            if (str.includes('\n\n')) {
              // Found the header boundary.
              const split = str.split(/\n\n/);
              header += split.shift();
              const remaining = split.join('\n\n');
              const buf = Buffer.from(remaining, 'utf8');
              stream.removeListener('error', callback);
              // Remove the 'readable' listener before unshifting.
              stream.removeListener('readable', onReadable);
              if (buf.length)
                stream.unshift(buf);
              // Now the body of the message can be read from the stream.
              callback(null, header, stream);
              return;
            }
            // Still reading the header.
            header += str;
          }
        }
      }
      ```

      Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

      @param chunk

      Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

      @param encoding

      Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
    - [wrap](https://bun.com/reference/node/stream/default/Transform/wrap)(

      stream: ReadableStream

      ): this;

      Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

      When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

      It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

      ```
      import { OldReader } from './old-api-module.js';
      import { Readable } from 'node:stream';
      const oreader = new OldReader();
      const myReader = new Readable().wrap(oreader);

      myReader.on('readable', () => {
        myReader.read(); // etc.
      });
      ```

      @param stream

      An "old style" readable stream
    - [write](https://bun.com/reference/node/stream/default/Transform/write)(

      chunk: any,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

      [write](https://bun.com/reference/node/stream/default/Transform/write)(

      chunk: any,

      encoding: BufferEncoding,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding, if `chunk` is a string.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
    - static [addAbortListener](https://bun.com/reference/node/stream/default/Transform/addAbortListener)(

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
    - static [from](https://bun.com/reference/node/stream/default/Transform/from)(

      src: string | Object | [Stream](https://bun.com/reference/node/stream/default) | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | [Blob](https://bun.com/reference/node/buffer/Blob) | Promise<any> | Iterable<any, any, any> | AsyncIterable<any, any, any> | AsyncGeneratorFunction

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating duplex streams.

      * `Stream` converts writable stream into writable `Duplex` and readable stream to `Duplex`.
      * `Blob` converts into readable `Duplex`.
      * `string` converts into readable `Duplex`.
      * `ArrayBuffer` converts into readable `Duplex`.
      * `AsyncIterable` converts into a readable `Duplex`. Cannot yield `null`.
      * `AsyncGeneratorFunction` converts into a readable/writable transform `Duplex`. Must take a source `AsyncIterable` as first parameter. Cannot yield `null`.
      * `AsyncFunction` converts into a writable `Duplex`. Must return either `null` or `undefined`
      * `Object ({ writable, readable })` converts `readable` and `writable` into `Stream` and then combines them into `Duplex` where the `Duplex` will write to the `writable` and read from the `readable`.
      * `Promise` converts into readable `Duplex`. Value `null` is ignored.
    - static [fromWeb](https://bun.com/reference/node/stream/default/Transform/fromWeb)(

      duplexStream: { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) },

      options?: Pick<[DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>, 'signal' | 'allowHalfOpen' | 'decodeStrings' | 'encoding' | 'highWaterMark' | 'objectMode'>

      ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

      A utility method for creating a `Duplex` from a web `ReadableStream` and `WritableStream`.
    - static [getEventListeners](https://bun.com/reference/node/stream/default/Transform/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/stream/default/Transform/getMaxListeners)(

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
    - static [on](https://bun.com/reference/node/stream/default/Transform/on)(

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

      static [on](https://bun.com/reference/node/stream/default/Transform/on)(

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
    - static [once](https://bun.com/reference/node/stream/default/Transform/once)(

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

      static [once](https://bun.com/reference/node/stream/default/Transform/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/stream/default/Transform/setMaxListeners)(

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
    - static [toWeb](https://bun.com/reference/node/stream/default/Transform/toWeb)(

      streamDuplex: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

      ): { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) };

      A utility method for creating a web `ReadableStream` and `WritableStream` from a `Duplex`.
  + ### class [Writable](https://bun.com/reference/node/stream/default/Writable)

    - readonly [closed](https://bun.com/reference/node/stream/default/Writable/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/stream/default/Writable/destroyed): boolean

      Is `true` after `writable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/stream/default/Writable/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - readonly [writable](https://bun.com/reference/node/stream/default/Writable/writable): boolean

      Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
    - readonly [writableAborted](https://bun.com/reference/node/stream/default/Writable/writableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'finish'`.
    - readonly [writableCorked](https://bun.com/reference/node/stream/default/Writable/writableCorked): number

      Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
    - readonly [writableEnded](https://bun.com/reference/node/stream/default/Writable/writableEnded): boolean

      Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
    - readonly [writableFinished](https://bun.com/reference/node/stream/default/Writable/writableFinished): boolean

      Is set to `true` immediately before the `'finish'` event is emitted.
    - readonly [writableHighWaterMark](https://bun.com/reference/node/stream/default/Writable/writableHighWaterMark): number

      Return the value of `highWaterMark` passed when creating this `Writable`.
    - readonly [writableLength](https://bun.com/reference/node/stream/default/Writable/writableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [writableNeedDrain](https://bun.com/reference/node/stream/default/Writable/writableNeedDrain): boolean

      Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
    - readonly [writableObjectMode](https://bun.com/reference/node/stream/default/Writable/writableObjectMode): boolean

      Getter for the property `objectMode` of a given `Writable` stream.
    - static [captureRejections](https://bun.com/reference/node/stream/default/Writable/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/Writable/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/stream/default/Writable/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/stream/default/Writable/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [\_construct](https://bun.com/reference/node/stream/default/Writable/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/stream/default/Writable/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_final](https://bun.com/reference/node/stream/default/Writable/_final)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_write](https://bun.com/reference/node/stream/default/Writable/_write)(

      chunk: any,

      encoding: BufferEncoding,

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_writev](https://bun.com/reference/node/stream/default/Writable/_writev)(

      chunks: { chunk: any; encoding: BufferEncoding }[],

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/default/Writable/[asyncDispose])(): Promise<void>;

      Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/Writable/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'close',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'drain',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'finish',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe

      [addListener](https://bun.com/reference/node/stream/default/Writable/addListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. drain
      3. error
      4. finish
      5. pipe
      6. unpipe
    - [compose](https://bun.com/reference/node/stream/default/Writable/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [cork](https://bun.com/reference/node/stream/default/Writable/cork)(): void;

      The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

      The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

      See also: `writable.uncork()`, `writable._writev()`.
    - [destroy](https://bun.com/reference/node/stream/default/Writable/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `writable._destroy()`.

      @param error

      Optional, an error to emit with `'error'` event.
    - [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'close'

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

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'drain'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'error',

      err: [Error](https://bun.com/reference/globals/Error)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'finish'

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'pipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: 'unpipe',

      src: [Readable](https://bun.com/reference/node/stream/default/Readable)

      ): boolean;

      [emit](https://bun.com/reference/node/stream/default/Writable/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [end](https://bun.com/reference/node/stream/default/Writable/end)(

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      [end](https://bun.com/reference/node/stream/default/Writable/end)(

      chunk: any,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      [end](https://bun.com/reference/node/stream/default/Writable/end)(

      chunk: any,

      encoding: BufferEncoding,

      cb?: () => void

      ): this;

      Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

      Calling the write method after calling end will raise an error.

      ```
      // Write 'hello, ' and then end with 'world!'.
      import fs from 'node:fs';
      const file = fs.createWriteStream('example.txt');
      file.write('hello, ');
      file.end('world!');
      // Writing more now is not allowed!
      ```

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding if `chunk` is a string
    - [eventNames](https://bun.com/reference/node/stream/default/Writable/eventNames)(): string | symbol[];

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
    - [getMaxListeners](https://bun.com/reference/node/stream/default/Writable/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [listenerCount](https://bun.com/reference/node/stream/default/Writable/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/stream/default/Writable/listeners)<K>(

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
    - [off](https://bun.com/reference/node/stream/default/Writable/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'close',

      listener: () => void

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

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'drain',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'finish',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [on](https://bun.com/reference/node/stream/default/Writable/on)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'close',

      listener: () => void

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

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'drain',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'finish',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [once](https://bun.com/reference/node/stream/default/Writable/once)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [pipe](https://bun.com/reference/node/stream/default/Writable/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'close',

      listener: () => void

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

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/stream/default/Writable/prependListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'close',

      listener: () => void

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

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/stream/default/Writable/prependOnceListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [rawListeners](https://bun.com/reference/node/stream/default/Writable/rawListeners)<K>(

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
    - [removeAllListeners](https://bun.com/reference/node/stream/default/Writable/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'close',

      listener: () => void

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

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'drain',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'finish',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'pipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: 'unpipe',

      listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/stream/default/Writable/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [setDefaultEncoding](https://bun.com/reference/node/stream/default/Writable/setDefaultEncoding)(

      encoding: BufferEncoding

      ): this;

      The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

      @param encoding

      The new default encoding
    - [setMaxListeners](https://bun.com/reference/node/stream/default/Writable/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [uncork](https://bun.com/reference/node/stream/default/Writable/uncork)(): void;

      The `writable.uncork()` method flushes all data buffered since cork was called.

      When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

      ```
      stream.cork();
      stream.write('some ');
      stream.write('data ');
      process.nextTick(() => stream.uncork());
      ```

      If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

      ```
      stream.cork();
      stream.write('some ');
      stream.cork();
      stream.write('data ');
      process.nextTick(() => {
        stream.uncork();
        // The data will not be flushed until uncork() is called a second time.
        stream.uncork();
      });
      ```

      See also: `writable.cork()`.
    - [write](https://bun.com/reference/node/stream/default/Writable/write)(

      chunk: any,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

      [write](https://bun.com/reference/node/stream/default/Writable/write)(

      chunk: any,

      encoding: BufferEncoding,

      callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

      ): boolean;

      The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

      The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

      While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

      Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

      If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

      ```
      function write(data, cb) {
        if (!stream.write(data)) {
          stream.once('drain', cb);
        } else {
          process.nextTick(cb);
        }
      }

      // Wait for cb to be called before doing any other write.
      write('hello', () => {
        console.log('Write completed, do more writes now.');
      });
      ```

      A `Writable` stream in object mode will always ignore the `encoding` argument.

      @param chunk

      Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

      @param encoding

      The encoding, if `chunk` is a string.

      @param callback

      Callback for when this chunk of data is flushed.

      @returns

      `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
    - static [addAbortListener](https://bun.com/reference/node/stream/default/Writable/addAbortListener)(

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
    - static [fromWeb](https://bun.com/reference/node/stream/default/Writable/fromWeb)(

      writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

      options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

      ): [Writable](https://bun.com/reference/node/stream/default/Writable);

      A utility method for creating a `Writable` from a web `WritableStream`.
    - static [getEventListeners](https://bun.com/reference/node/stream/default/Writable/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/stream/default/Writable/getMaxListeners)(

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
    - static [on](https://bun.com/reference/node/stream/default/Writable/on)(

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

      static [on](https://bun.com/reference/node/stream/default/Writable/on)(

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
    - static [once](https://bun.com/reference/node/stream/default/Writable/once)(

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

      static [once](https://bun.com/reference/node/stream/default/Writable/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/stream/default/Writable/setMaxListeners)(

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
    - static [toWeb](https://bun.com/reference/node/stream/default/Writable/toWeb)(

      streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

      ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

      A utility method for creating a web `WritableStream` from a `Writable`.
  + ### interface [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    - [concurrency](https://bun.com/reference/node/stream/default/ArrayOptions/concurrency)?: number

      The maximum concurrent invocations of `fn` to call on the stream at once.
    - [signal](https://bun.com/reference/node/stream/default/ArrayOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      Allows destroying the stream if the signal is aborted.
  + ### interface [DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<T extends [Duplex](https://bun.com/reference/node/stream/default/Duplex) = [Duplex](https://bun.com/reference/node/stream/default/Duplex)>

    - [allowHalfOpen](https://bun.com/reference/node/stream/default/DuplexOptions/allowHalfOpen)?: boolean
    - [autoDestroy](https://bun.com/reference/node/stream/default/DuplexOptions/autoDestroy)?: boolean
    - [construct](https://bun.com/reference/node/stream/default/DuplexOptions/construct)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [decodeStrings](https://bun.com/reference/node/stream/default/DuplexOptions/decodeStrings)?: boolean
    - [defaultEncoding](https://bun.com/reference/node/stream/default/DuplexOptions/defaultEncoding)?: BufferEncoding
    - [destroy](https://bun.com/reference/node/stream/default/DuplexOptions/destroy)?: (this: T, error: null | [Error](https://bun.com/reference/globals/Error), callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [emitClose](https://bun.com/reference/node/stream/default/DuplexOptions/emitClose)?: boolean
    - [encoding](https://bun.com/reference/node/stream/default/DuplexOptions/encoding)?: BufferEncoding
    - [final](https://bun.com/reference/node/stream/default/DuplexOptions/final)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [highWaterMark](https://bun.com/reference/node/stream/default/DuplexOptions/highWaterMark)?: number
    - [objectMode](https://bun.com/reference/node/stream/default/DuplexOptions/objectMode)?: boolean
    - [read](https://bun.com/reference/node/stream/default/DuplexOptions/read)?: (this: T, size: number) => void
    - [readableHighWaterMark](https://bun.com/reference/node/stream/default/DuplexOptions/readableHighWaterMark)?: number
    - [readableObjectMode](https://bun.com/reference/node/stream/default/DuplexOptions/readableObjectMode)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/DuplexOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
    - [writableCorked](https://bun.com/reference/node/stream/default/DuplexOptions/writableCorked)?: number
    - [writableHighWaterMark](https://bun.com/reference/node/stream/default/DuplexOptions/writableHighWaterMark)?: number
    - [writableObjectMode](https://bun.com/reference/node/stream/default/DuplexOptions/writableObjectMode)?: boolean
    - [write](https://bun.com/reference/node/stream/default/DuplexOptions/write)?: (this: T, chunk: any, encoding: BufferEncoding, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [writev](https://bun.com/reference/node/stream/default/DuplexOptions/writev)?: (this: T, chunks: { chunk: any; encoding: BufferEncoding }[], callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
  + ### interface [FinishedOptions](https://bun.com/reference/node/stream/default/FinishedOptions)

    - [error](https://bun.com/reference/node/stream/default/FinishedOptions/error)?: boolean
    - [readable](https://bun.com/reference/node/stream/default/FinishedOptions/readable)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/FinishedOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
    - [writable](https://bun.com/reference/node/stream/default/FinishedOptions/writable)?: boolean
  + ### interface [Pipe](https://bun.com/reference/node/stream/default/Pipe)

    - [close](https://bun.com/reference/node/stream/default/Pipe/close)(): void;
    - [hasRef](https://bun.com/reference/node/stream/default/Pipe/hasRef)(): boolean;
    - [ref](https://bun.com/reference/node/stream/default/Pipe/ref)(): void;
    - [unref](https://bun.com/reference/node/stream/default/Pipe/unref)(): void;
  + ### interface [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

    - [end](https://bun.com/reference/node/stream/default/PipelineOptions/end)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/PipelineOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + ### interface [ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<T extends [Readable](https://bun.com/reference/node/stream/default/Readable) = [Readable](https://bun.com/reference/node/stream/default/Readable)>

    - [autoDestroy](https://bun.com/reference/node/stream/default/ReadableOptions/autoDestroy)?: boolean
    - [construct](https://bun.com/reference/node/stream/default/ReadableOptions/construct)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [destroy](https://bun.com/reference/node/stream/default/ReadableOptions/destroy)?: (this: T, error: null | [Error](https://bun.com/reference/globals/Error), callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [emitClose](https://bun.com/reference/node/stream/default/ReadableOptions/emitClose)?: boolean
    - [encoding](https://bun.com/reference/node/stream/default/ReadableOptions/encoding)?: BufferEncoding
    - [highWaterMark](https://bun.com/reference/node/stream/default/ReadableOptions/highWaterMark)?: number
    - [objectMode](https://bun.com/reference/node/stream/default/ReadableOptions/objectMode)?: boolean
    - [read](https://bun.com/reference/node/stream/default/ReadableOptions/read)?: (this: T, size: number) => void
    - [signal](https://bun.com/reference/node/stream/default/ReadableOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + ### interface [StreamOptions](https://bun.com/reference/node/stream/default/StreamOptions)<T extends [Stream](https://bun.com/reference/node/stream/default)>

    - [autoDestroy](https://bun.com/reference/node/stream/default/StreamOptions/autoDestroy)?: boolean
    - [construct](https://bun.com/reference/node/stream/default/StreamOptions/construct)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [destroy](https://bun.com/reference/node/stream/default/StreamOptions/destroy)?: (this: T, error: null | [Error](https://bun.com/reference/globals/Error), callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [emitClose](https://bun.com/reference/node/stream/default/StreamOptions/emitClose)?: boolean
    - [highWaterMark](https://bun.com/reference/node/stream/default/StreamOptions/highWaterMark)?: number
    - [objectMode](https://bun.com/reference/node/stream/default/StreamOptions/objectMode)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/StreamOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + ### interface [TransformOptions](https://bun.com/reference/node/stream/default/TransformOptions)<T extends [Transform](https://bun.com/reference/node/stream/default/Transform) = [Transform](https://bun.com/reference/node/stream/default/Transform)>

    - [allowHalfOpen](https://bun.com/reference/node/stream/default/TransformOptions/allowHalfOpen)?: boolean
    - [autoDestroy](https://bun.com/reference/node/stream/default/TransformOptions/autoDestroy)?: boolean
    - [construct](https://bun.com/reference/node/stream/default/TransformOptions/construct)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [decodeStrings](https://bun.com/reference/node/stream/default/TransformOptions/decodeStrings)?: boolean
    - [defaultEncoding](https://bun.com/reference/node/stream/default/TransformOptions/defaultEncoding)?: BufferEncoding
    - [destroy](https://bun.com/reference/node/stream/default/TransformOptions/destroy)?: (this: T, error: null | [Error](https://bun.com/reference/globals/Error), callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [emitClose](https://bun.com/reference/node/stream/default/TransformOptions/emitClose)?: boolean
    - [encoding](https://bun.com/reference/node/stream/default/TransformOptions/encoding)?: BufferEncoding
    - [final](https://bun.com/reference/node/stream/default/TransformOptions/final)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [flush](https://bun.com/reference/node/stream/default/TransformOptions/flush)?: (this: T, callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)) => void
    - [highWaterMark](https://bun.com/reference/node/stream/default/TransformOptions/highWaterMark)?: number
    - [objectMode](https://bun.com/reference/node/stream/default/TransformOptions/objectMode)?: boolean
    - [read](https://bun.com/reference/node/stream/default/TransformOptions/read)?: (this: T, size: number) => void
    - [readableHighWaterMark](https://bun.com/reference/node/stream/default/TransformOptions/readableHighWaterMark)?: number
    - [readableObjectMode](https://bun.com/reference/node/stream/default/TransformOptions/readableObjectMode)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/TransformOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
    - [transform](https://bun.com/reference/node/stream/default/TransformOptions/transform)?: (this: T, chunk: any, encoding: BufferEncoding, callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)) => void
    - [writableCorked](https://bun.com/reference/node/stream/default/TransformOptions/writableCorked)?: number
    - [writableHighWaterMark](https://bun.com/reference/node/stream/default/TransformOptions/writableHighWaterMark)?: number
    - [writableObjectMode](https://bun.com/reference/node/stream/default/TransformOptions/writableObjectMode)?: boolean
    - [write](https://bun.com/reference/node/stream/default/TransformOptions/write)?: (this: T, chunk: any, encoding: BufferEncoding, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [writev](https://bun.com/reference/node/stream/default/TransformOptions/writev)?: (this: T, chunks: { chunk: any; encoding: BufferEncoding }[], callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
  + ### interface [WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<T extends [Writable](https://bun.com/reference/node/stream/default/Writable) = [Writable](https://bun.com/reference/node/stream/default/Writable)>

    - [autoDestroy](https://bun.com/reference/node/stream/default/WritableOptions/autoDestroy)?: boolean
    - [construct](https://bun.com/reference/node/stream/default/WritableOptions/construct)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [decodeStrings](https://bun.com/reference/node/stream/default/WritableOptions/decodeStrings)?: boolean
    - [defaultEncoding](https://bun.com/reference/node/stream/default/WritableOptions/defaultEncoding)?: BufferEncoding
    - [destroy](https://bun.com/reference/node/stream/default/WritableOptions/destroy)?: (this: T, error: null | [Error](https://bun.com/reference/globals/Error), callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [emitClose](https://bun.com/reference/node/stream/default/WritableOptions/emitClose)?: boolean
    - [final](https://bun.com/reference/node/stream/default/WritableOptions/final)?: (this: T, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [highWaterMark](https://bun.com/reference/node/stream/default/WritableOptions/highWaterMark)?: number
    - [objectMode](https://bun.com/reference/node/stream/default/WritableOptions/objectMode)?: boolean
    - [signal](https://bun.com/reference/node/stream/default/WritableOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
    - [write](https://bun.com/reference/node/stream/default/WritableOptions/write)?: (this: T, chunk: any, encoding: BufferEncoding, callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
    - [writev](https://bun.com/reference/node/stream/default/WritableOptions/writev)?: (this: T, chunks: { chunk: any; encoding: BufferEncoding }[], callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void) => void
  + type [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<S extends [PipelineDestination](https://bun.com/reference/node/stream/default/PipelineDestination)<any, any>> = S extends [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, infer P> ? (err: NodeJS.ErrnoException | null, value: P) => void : (err: NodeJS.ErrnoException | null) => void
  + type [PipelineDestination](https://bun.com/reference/node/stream/default/PipelineDestination)<S extends [PipelineTransformSource](https://bun.com/reference/node/stream/default/PipelineTransformSource)<any>, P> = S extends [PipelineTransformSource](https://bun.com/reference/node/stream/default/PipelineTransformSource)<infer ST> ? NodeJS.WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<ST> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<ST, P> : never
  + type [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<T> = (source: AsyncIterable<T>) => AsyncIterable<any>
  + type [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<T, P> = (source: AsyncIterable<T>) => Promise<P>
  + type [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<S extends [PipelineDestination](https://bun.com/reference/node/stream/default/PipelineDestination)<any, any>> = S extends [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, infer P> ? Promise<P> : Promise<void>
  + type [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<T> = Iterable<T> | AsyncIterable<T> | NodeJS.ReadableStream | [PipelineSourceFunction](https://bun.com/reference/node/stream/default/PipelineSourceFunction)<T>
  + type [PipelineSourceFunction](https://bun.com/reference/node/stream/default/PipelineSourceFunction)<T> = () => Iterable<T> | AsyncIterable<T>
  + type [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<S extends [PipelineTransformSource](https://bun.com/reference/node/stream/default/PipelineTransformSource)<any>, U> = NodeJS.ReadWriteStream | (source: S extends (...args: any[]) => Iterable<infer ST> | AsyncIterable<infer ST> ? AsyncIterable<ST> : S) => AsyncIterable<U>
  + type [PipelineTransformSource](https://bun.com/reference/node/stream/default/PipelineTransformSource)<T> = [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<T> | [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<any, T>
  + type [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback) = (error?: [Error](https://bun.com/reference/globals/Error) | null, data?: any) => void
  + function [addAbortSignal](https://bun.com/reference/node/stream/default/addAbortSignal)<T extends [Stream](https://bun.com/reference/node/stream/default)>(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    stream: T

    ): T;

    A stream to attach a signal to.

    Attaches an AbortSignal to a readable or writeable stream. This lets code control stream destruction using an `AbortController`.

    Calling `abort` on the `AbortController` corresponding to the passed `AbortSignal` will behave the same way as calling `.destroy(new AbortError())` on the stream, and `controller.error(new AbortError())` for webstreams.

    ```
    import fs from 'node:fs';

    const controller = new AbortController();
    const read = addAbortSignal(
      controller.signal,
      fs.createReadStream(('object.json')),
    );
    // Later, abort the operation closing the stream
    controller.abort();
    ```

    Or using an `AbortSignal` with a readable stream as an async iterable:

    ```
    const controller = new AbortController();
    setTimeout(() => controller.abort(), 10_000); // set a timeout
    const stream = addAbortSignal(
      controller.signal,
      fs.createReadStream(('object.json')),
    );
    (async () => {
      try {
        for await (const chunk of stream) {
          await process(chunk);
        }
      } catch (e) {
        if (e.name === 'AbortError') {
          // The operation was cancelled
        } else {
          throw e;
        }
      }
    })();
    ```

    Or using an `AbortSignal` with a ReadableStream:

    ```
    const controller = new AbortController();
    const rs = new ReadableStream({
      start(controller) {
        controller.enqueue('hello');
        controller.enqueue('world');
        controller.close();
      },
    });

    addAbortSignal(controller.signal, rs);

    finished(rs, (err) => {
      if (err) {
        if (err.name === 'AbortError') {
          // The operation was cancelled
        }
      }
    });

    const reader = rs.getReader();

    reader.read().then(({ value, done }) => {
      console.log(value); // hello
      console.log(done); // false
      controller.abort();
    });
    ```

    @param signal

    A signal representing possible cancellation

    @param stream

    A stream to attach a signal to.
  + function [duplexPair](https://bun.com/reference/node/stream/default/duplexPair)(

    options?: [DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>

    ): [[Duplex](https://bun.com/reference/node/stream/default/Duplex), [Duplex](https://bun.com/reference/node/stream/default/Duplex)];

    The utility function `duplexPair` returns an Array with two items, each being a `Duplex` stream connected to the other side:

    ```
    const [ sideA, sideB ] = duplexPair();
    ```

    Whatever is written to one stream is made readable on the other. It provides behavior analogous to a network connection, where the data written by the client becomes readable by the server, and vice-versa.

    The Duplex streams are symmetrical; one or the other may be used without any difference in behavior.

    @param options

    A value to pass to both Duplex constructors, to set options such as buffering.
  + function [finished](https://bun.com/reference/node/stream/default/finished)(

    stream: ReadWriteStream | ReadableStream | WritableStream,

    options: [FinishedOptions](https://bun.com/reference/node/stream/default/FinishedOptions),

    callback: (err?: null | ErrnoException) => void

    ): () => void;

    A readable and/or writable stream/webstream.

    A function to get notified when a stream is no longer readable, writable or has experienced an error or a premature close event.

    ```
    import { finished } from 'node:stream';
    import fs from 'node:fs';

    const rs = fs.createReadStream('archive.tar');

    finished(rs, (err) => {
      if (err) {
        console.error('Stream failed.', err);
      } else {
        console.log('Stream is done reading.');
      }
    });

    rs.resume(); // Drain the stream.
    ```

    Especially useful in error handling scenarios where a stream is destroyed prematurely (like an aborted HTTP request), and will not emit `'end'` or `'finish'`.

    The `finished` API provides [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streamfinishedstream-options).

    `stream.finished()` leaves dangling event listeners (in particular `'error'`, `'end'`, `'finish'` and `'close'`) after `callback` has been invoked. The reason for this is so that unexpected `'error'` events (due to incorrect stream implementations) do not cause unexpected crashes. If this is unwanted behavior then the returned cleanup function needs to be invoked in the callback:

    ```
    const cleanup = finished(rs, (err) => {
      cleanup();
      // ...
    });
    ```

    @param stream

    A readable and/or writable stream.

    @param callback

    A callback function that takes an optional error argument.

    @returns

    A cleanup function which removes all registered listeners.

    function [finished](https://bun.com/reference/node/stream/default/finished)(

    stream: ReadWriteStream | ReadableStream | WritableStream,

    callback: (err?: null | ErrnoException) => void

    ): () => void;

    A readable and/or writable stream/webstream.

    A function to get notified when a stream is no longer readable, writable or has experienced an error or a premature close event.

    ```
    import { finished } from 'node:stream';
    import fs from 'node:fs';

    const rs = fs.createReadStream('archive.tar');

    finished(rs, (err) => {
      if (err) {
        console.error('Stream failed.', err);
      } else {
        console.log('Stream is done reading.');
      }
    });

    rs.resume(); // Drain the stream.
    ```

    Especially useful in error handling scenarios where a stream is destroyed prematurely (like an aborted HTTP request), and will not emit `'end'` or `'finish'`.

    The `finished` API provides [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streamfinishedstream-options).

    `stream.finished()` leaves dangling event listeners (in particular `'error'`, `'end'`, `'finish'` and `'close'`) after `callback` has been invoked. The reason for this is so that unexpected `'error'` events (due to incorrect stream implementations) do not cause unexpected crashes. If this is unwanted behavior then the returned cleanup function needs to be invoked in the callback:

    ```
    const cleanup = finished(rs, (err) => {
      cleanup();
      // ...
    });
    ```

    @param stream

    A readable and/or writable stream.

    @param callback

    A callback function that takes an optional error argument.

    @returns

    A cleanup function which removes all registered listeners.
  + function [getDefaultHighWaterMark](https://bun.com/reference/node/stream/default/getDefaultHighWaterMark)(

    objectMode: boolean

    ): number;

    Returns the default highWaterMark used by streams. Defaults to `65536` (64 KiB), or `16` for `objectMode`.
  + function [isErrored](https://bun.com/reference/node/stream/default/isErrored)(

    stream: [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream | WritableStream

    ): boolean;

    Returns whether the stream has encountered an error.
  + function [isReadable](https://bun.com/reference/node/stream/default/isReadable)(

    stream: [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream

    ): null | boolean;

    Returns whether the stream is readable.

    @returns

    Only returns `null` if `stream` is not a valid `Readable`, `Duplex` or `ReadableStream`.
  + function [isWritable](https://bun.com/reference/node/stream/default/isWritable)(

    stream: [Writable](https://bun.com/reference/node/stream/default/Writable) | WritableStream

    ): null | boolean;

    Returns whether the stream is writable.

    @returns

    Only returns `null` if `stream` is not a valid `Writable`, `Duplex` or `WritableStream`.
  + function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    transform3: T3,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, T4 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T3, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

    source: A,

    transform1: T1,

    transform2: T2,

    transform3: T3,

    transform4: T4,

    destination: B,

    callback: [PipelineCallback](https://bun.com/reference/node/stream/default/PipelineCallback)<B>

    ): B extends WritableStream ? B<B> : WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)(

    streams: readonly ReadWriteStream | ReadableStream | WritableStream[],

    callback: (err: null | ErrnoException) => void

    ): WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```

    @param callback

    Called when the pipeline is fully done.

    function [pipeline](https://bun.com/reference/node/stream/default/pipeline)(

    stream1: ReadableStream,

    stream2: ReadWriteStream | WritableStream,

    ...streams: ReadWriteStream | WritableStream | (err: null | ErrnoException) => void[]

    ): WritableStream;

    A module method to pipe between streams and generators forwarding errors and properly cleaning up and provide a callback when the pipeline is complete.

    ```
    import { pipeline } from 'node:stream';
    import fs from 'node:fs';
    import zlib from 'node:zlib';

    // Use the pipeline API to easily pipe a series of streams
    // together and get notified when the pipeline is fully done.

    // A pipeline to gzip a potentially huge tar file efficiently:

    pipeline(
      fs.createReadStream('archive.tar'),
      zlib.createGzip(),
      fs.createWriteStream('archive.tar.gz'),
      (err) => {
        if (err) {
          console.error('Pipeline failed.', err);
        } else {
          console.log('Pipeline succeeded.');
        }
      },
    );
    ```

    The `pipeline` API provides a [`promise version`](https://nodejs.org/docs/latest-v24.x/api/stream.html#streampipelinesource-transforms-destination-options).

    `stream.pipeline()` will call `stream.destroy(err)` on all streams except:

    - `Readable` streams which have emitted `'end'` or `'close'`.
    - `Writable` streams which have emitted `'finish'` or `'close'`.

    `stream.pipeline()` leaves dangling event listeners on the streams after the `callback` has been invoked. In the case of reuse of streams after failure, this can cause event listener leaks and swallowed errors. If the last stream is readable, dangling event listeners will be removed so that the last stream can be consumed later.

    `stream.pipeline()` closes all the streams when an error is raised. The `IncomingRequest` usage with `pipeline` could lead to an unexpected behavior once it would destroy the socket without sending the expected response. See the example below:

    ```
    import fs from 'node:fs';
    import http from 'node:http';
    import { pipeline } from 'node:stream';

    const server = http.createServer((req, res) => {
      const fileStream = fs.createReadStream('./fileNotExist.txt');
      pipeline(fileStream, res, (err) => {
        if (err) {
          console.log(err); // No such file
          // this message can't be sent once `pipeline` already destroyed the socket
          return res.end('error!!!');
        }
      });
    });
    ```
  + function [setDefaultHighWaterMark](https://bun.com/reference/node/stream/default/setDefaultHighWaterMark)(

    objectMode: boolean,

    value: number

    ): void;

    Sets the default highWaterMark used by streams.

    @param value

    highWaterMark value
* ### class [default](https://bun.com/reference/node/stream/default)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + static [captureRejections](https://bun.com/reference/node/stream/default/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/stream/default/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/stream/default/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/stream/default/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/stream/default/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/stream/default/addListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [compose](https://bun.com/reference/node/stream/default/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [emit](https://bun.com/reference/node/stream/default/emit)<K>(

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
  + [eventNames](https://bun.com/reference/node/stream/default/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/stream/default/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/stream/default/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/stream/default/listeners)<K>(

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
  + [off](https://bun.com/reference/node/stream/default/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/stream/default/on)<K>(

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
  + [once](https://bun.com/reference/node/stream/default/once)<K>(

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
  + [pipe](https://bun.com/reference/node/stream/default/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/stream/default/prependListener)<K>(

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
  + [prependOnceListener](https://bun.com/reference/node/stream/default/prependOnceListener)<K>(

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
  + [rawListeners](https://bun.com/reference/node/stream/default/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/stream/default/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/stream/default/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/stream/default/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/stream/default/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/stream/default/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/stream/default/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/stream/default/on)(

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

    static [on](https://bun.com/reference/node/stream/default/on)(

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
  + static [once](https://bun.com/reference/node/stream/default/once)(

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

    static [once](https://bun.com/reference/node/stream/default/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/stream/default/setMaxListeners)(

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