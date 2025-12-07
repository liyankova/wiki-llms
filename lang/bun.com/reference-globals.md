---
url: https://bun.com/reference/globals
title: globals module | API Reference | Bun
source_domain: bun.com
---

# globals module | API Reference | Bun

module

# [globals](https://bun.com/reference/globals)

* function [fetch](https://bun.com/reference/globals/fetch)(

  input: string | [URL](https://bun.com/reference/globals/URL) | [Request](https://bun.com/reference/globals/Request),

  init?: [BunFetchRequestInit](https://bun.com/reference/globals/BunFetchRequestInit)

  ): Promise<[Response](https://bun.com/reference/globals/Response)>;

  Send a HTTP(s) request

  @param input

  URL string or Request object

  @param init

  A structured value that contains settings for the fetch() request.

  @returns

  A promise that resolves to Response object.

  ### namespace [fetch](https://bun.com/reference/globals/fetch)

  Bun's extensions of the `fetch` API

  + function [preconnect](https://bun.com/reference/globals/fetch/preconnect)(

    url: string | [URL](https://bun.com/reference/globals/URL),

    options?: { dns: boolean; http: boolean; https: boolean; tcp: boolean }

    ): void;

    Preconnect to a URL. This can be used to improve performance by pre-resolving the DNS and establishing a TCP connection before the request is made.

    This is a custom property that is not part of the Fetch API specification.

    @param url

    The URL to preconnect to

    @param options

    Options for the preconnect
* function [setImmediate](https://bun.com/reference/globals/setImmediate)(

  handler: [TimerHandler](https://bun.com/reference/bun/TimerHandler),

  ...arguments: any[]

  ): [Timer](https://bun.com/reference/globals/Timer);

  Run a function immediately after main event loop is vacant

  @param handler

  function to call

  ### namespace [setImmediate](https://bun.com/reference/globals/setImmediate)
* function [setTimeout](https://bun.com/reference/globals/setTimeout)(

  handler: TimerHandler,

  timeout?: number,

  ...arguments: any[]

  ): number;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/setTimeout)

  ### namespace [setTimeout](https://bun.com/reference/globals/setTimeout)
* const [console](https://bun.com/reference/globals/console): [Console](https://bun.com/reference/globals/Console)
* const [crypto](https://bun.com/reference/globals/crypto): [Crypto](https://bun.com/reference/globals/Crypto)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/crypto)
* const [Error](https://bun.com/reference/globals/Error): [ErrorConstructor](https://bun.com/reference/globals/ErrorConstructor)
* const [exports](https://bun.com/reference/globals/exports): any

  Same as module.exports
* const [Loader](https://bun.com/reference/globals/Loader): { dependencyKeysIfEvaluated: (specifier: string) => string[]; registry: Map<string, { dependencies: typeof [Loader](https://bun.com/reference/globals/Loader)['registry'] extends Map<any, infer V> ? V : any[]; evaluated: boolean; fetch: Promise<any>; instantiate: Promise<any>; isAsync: boolean; key: string; linkError: any; linkSucceeded: boolean; module: { dependenciesMap: typeof [Loader](https://bun.com/reference/globals/Loader)['registry'] }; satisfy: Promise<any>; state: number; then: any }>; resolve: (specifier: string, referrer: string) => string }

  Low-level JavaScriptCore API for accessing the native ES Module loader (not a Bun API)

  Before using this, be aware of a few things:

  **Using this incorrectly will crash your application**.

  This API may change any time JavaScriptCore is updated.

  Bun may rewrite ESM import specifiers to point to bundled code. This will be confusing when using this API, as it will return a string like "/node\_modules.server.bun".

  Bun may inject additional imports into your code. This usually has a `bun:` prefix.
* const [module](https://bun.com/reference/globals/module): NodeModule

  A reference to the current module.
* const [navigator](https://bun.com/reference/globals/navigator): [Navigator](https://bun.com/reference/globals/Navigator)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/navigator)
* const [performance](https://bun.com/reference/globals/performance): [Performance](https://bun.com/reference/globals/Performance)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/performance)
* const [require](https://bun.com/reference/globals/require): NodeJS.Require

  NodeJS-style `require` function
* const [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer): SharedArrayBufferConstructor
* function [addEventListener](https://bun.com/reference/globals/addEventListener)<K extends keyof [EventMap](https://bun.com/reference/globals/EventMap)>(

  type: K,

  listener: (this: object, ev: [EventMap](https://bun.com/reference/globals/EventMap)[K]) => any,

  options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

  ): void;
* function [alert](https://bun.com/reference/globals/alert)(

  message?: string

  ): void;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/alert)
* function [clearImmediate](https://bun.com/reference/globals/clearImmediate)(

  id?: number | [Timer](https://bun.com/reference/globals/Timer)

  ): void;

  Cancel an immediate function call by its immediate ID.

  @param id

  immediate id
* function [clearInterval](https://bun.com/reference/globals/clearInterval)(

  id: undefined | number

  ): void;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/clearInterval)
* function [clearTimeout](https://bun.com/reference/globals/clearTimeout)(

  id: undefined | number

  ): void;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/clearTimeout)
* function [confirm](https://bun.com/reference/globals/confirm)(

  message?: string

  ): boolean;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/confirm)
* function [fetch](https://bun.com/reference/globals/fetch)(

  input: string | [URL](https://bun.com/reference/globals/URL) | [Request](https://bun.com/reference/globals/Request),

  init?: [BunFetchRequestInit](https://bun.com/reference/globals/BunFetchRequestInit)

  ): Promise<[Response](https://bun.com/reference/globals/Response)>;

  Send a HTTP(s) request

  @param input

  URL string or Request object

  @param init

  A structured value that contains settings for the fetch() request.

  @returns

  A promise that resolves to Response object.

  function [preconnect](https://bun.com/reference/globals/fetch/preconnect)(

  url: string | [URL](https://bun.com/reference/globals/URL),

  options?: { dns: boolean; http: boolean; https: boolean; tcp: boolean }

  ): void;

  Preconnect to a URL. This can be used to improve performance by pre-resolving the DNS and establishing a TCP connection before the request is made.

  This is a custom property that is not part of the Fetch API specification.

  @param url

  The URL to preconnect to

  @param options

  Options for the preconnect
* function [postMessage](https://bun.com/reference/globals/postMessage)(

  message: any,

  transfer?: [Transferable](https://bun.com/reference/bun/Transferable)[]

  ): void;

  Post a message to the parent thread.

  Only useful in a worker thread; calling this from the main thread does nothing.
* function [prompt](https://bun.com/reference/globals/prompt)(

  message?: string,

  \_default?: string

  ): null | string;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/prompt)
* function [queueMicrotask](https://bun.com/reference/globals/queueMicrotask)(

  callback: VoidFunction

  ): void;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/queueMicrotask)
* function [removeEventListener](https://bun.com/reference/globals/removeEventListener)<K extends keyof [EventMap](https://bun.com/reference/globals/EventMap)>(

  type: K,

  listener: (this: object, ev: [EventMap](https://bun.com/reference/globals/EventMap)[K]) => any,

  options?: boolean | [EventListenerOptions](https://bun.com/reference/bun/EventListenerOptions)

  ): void;
* function [reportError](https://bun.com/reference/globals/reportError)(

  error: any

  ): void;

  Log an error using the default exception handler

  @param error

  Error or string
* function [setImmediate](https://bun.com/reference/globals/setImmediate)(

  handler: [TimerHandler](https://bun.com/reference/bun/TimerHandler),

  ...arguments: any[]

  ): [Timer](https://bun.com/reference/globals/Timer);

  Run a function immediately after main event loop is vacant

  @param handler

  function to call
* function [setInterval](https://bun.com/reference/globals/setInterval)(

  handler: TimerHandler,

  timeout?: number,

  ...arguments: any[]

  ): number;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/setInterval)
* function [setTimeout](https://bun.com/reference/globals/setTimeout)(

  handler: TimerHandler,

  timeout?: number,

  ...arguments: any[]

  ): number;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/setTimeout)
* function [structuredClone](https://bun.com/reference/globals/structuredClone)<T = any>(

  value: T,

  options?: StructuredSerializeOptions

  ): T;

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Window/structuredClone)
* ### class [URL](https://bun.com/reference/globals/URL)

  The URL interface represents an object providing static methods used for creating object URLs.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL)

  + [hash](https://bun.com/reference/globals/URL/hash): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/hash)
  + [host](https://bun.com/reference/globals/URL/host): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/host)
  + [hostname](https://bun.com/reference/globals/URL/hostname): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/hostname)
  + [href](https://bun.com/reference/globals/URL/href): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/href)
  + readonly [origin](https://bun.com/reference/globals/URL/origin): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/origin)
  + [password](https://bun.com/reference/globals/URL/password): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/password)
  + [pathname](https://bun.com/reference/globals/URL/pathname): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/pathname)
  + [port](https://bun.com/reference/globals/URL/port): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/port)
  + [search](https://bun.com/reference/globals/URL/search): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/search)
  + readonly [searchParams](https://bun.com/reference/globals/URL/searchParams): [URLSearchParams](https://bun.com/reference/globals/URLSearchParams)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/searchParams)
  + [username](https://bun.com/reference/globals/URL/username): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/username)
  + [toJSON](https://bun.com/reference/globals/URL/toJSON)(): string;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/toJSON)
  + [toString](https://bun.com/reference/globals/URL/toString)(): string;

    The `toString()` method on the `URL` object returns the serialized URL. The value returned is equivalent to that of href and toJSON.
  + static [canParse](https://bun.com/reference/globals/URL/canParse)(

    url: string | [URL](https://bun.com/reference/globals/URL),

    base?: string | [URL](https://bun.com/reference/globals/URL)

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/canParse_static)
  + static [createObjectURL](https://bun.com/reference/globals/URL/createObjectURL)(

    obj: [Blob](https://bun.com/reference/globals/Blob) | MediaSource

    ): string;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/createObjectURL_static)
  + static [parse](https://bun.com/reference/globals/URL/parse)(

    url: string | [URL](https://bun.com/reference/globals/URL),

    base?: string | [URL](https://bun.com/reference/globals/URL)

    ): null | [URL](https://bun.com/reference/globals/URL);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/parse_static)
  + static [revokeObjectURL](https://bun.com/reference/globals/URL/revokeObjectURL)(

    url: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URL/revokeObjectURL_static)
* ### class [MessageEvent](https://bun.com/reference/globals/MessageEvent)<T = any>

  A message received by a target object.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/MessageEvent/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/MessageEvent/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/MessageEvent/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/MessageEvent/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/MessageEvent/CAPTURING_PHASE): 1
  + readonly [composed](https://bun.com/reference/globals/MessageEvent/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/MessageEvent/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [data](https://bun.com/reference/globals/MessageEvent/data): T

    Returns the data of the message.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent/data)
  + readonly [defaultPrevented](https://bun.com/reference/globals/MessageEvent/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [eventPhase](https://bun.com/reference/globals/MessageEvent/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [isTrusted](https://bun.com/reference/globals/MessageEvent/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [lastEventId](https://bun.com/reference/globals/MessageEvent/lastEventId): string

    Returns the last event ID string, for server-sent events.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent/lastEventId)
  + readonly [NONE](https://bun.com/reference/globals/MessageEvent/NONE): 0
  + readonly [origin](https://bun.com/reference/globals/MessageEvent/origin): string

    Returns the origin of the message, for server-sent events and cross-document messaging.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent/origin)
  + readonly [ports](https://bun.com/reference/globals/MessageEvent/ports): readonly [MessagePort](https://bun.com/reference/globals/MessagePort)[]

    Returns the MessagePort array sent with the message, for cross-document messaging and channel messaging.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent/ports)
  + [prototype](https://bun.com/reference/globals/MessageEvent/prototype): [MessageEvent](https://bun.com/reference/globals/MessageEvent)
  + readonly [source](https://bun.com/reference/globals/MessageEvent/source): null | MessageEventSource

    Returns the WindowProxy of the source window, for cross-document messaging, and the MessagePort being attached, in the connect event fired at SharedWorkerGlobalScope objects.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageEvent/source)
  + readonly [target](https://bun.com/reference/globals/MessageEvent/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/MessageEvent/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/MessageEvent/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + [composedPath](https://bun.com/reference/globals/MessageEvent/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/MessageEvent/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [stopImmediatePropagation](https://bun.com/reference/globals/MessageEvent/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/MessageEvent/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
* ### class [AbortController](https://bun.com/reference/globals/AbortController)

  A controller object that allows you to abort one or more DOM requests as and when desired.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortController)

  + readonly [signal](https://bun.com/reference/globals/AbortController/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Returns the AbortSignal object associated with this object.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortController/signal)
  + [abort](https://bun.com/reference/globals/AbortController/abort)(

    reason?: any

    ): void;
* ### class [AbortSignal](https://bun.com/reference/globals/AbortSignal)

  A signal object that allows you to communicate with a DOM request (such as a Fetch) and abort it if required via an AbortController object.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal)

  + readonly [aborted](https://bun.com/reference/globals/AbortSignal/aborted): boolean

    Returns true if this AbortSignal's AbortController has signaled to abort, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/aborted)
  + [onabort](https://bun.com/reference/globals/AbortSignal/onabort): null | (this: [AbortSignal](https://bun.com/reference/globals/AbortSignal), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/abort_event)
  + readonly [reason](https://bun.com/reference/globals/AbortSignal/reason): any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/reason)
  + [addEventListener](https://bun.com/reference/globals/AbortSignal/addEventListener)<K extends 'abort'>(

    type: K,

    listener: (this: [AbortSignal](https://bun.com/reference/globals/AbortSignal), ev: AbortSignalEventMap[K]) => any,

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
  + [dispatchEvent](https://bun.com/reference/globals/AbortSignal/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [removeEventListener](https://bun.com/reference/globals/AbortSignal/removeEventListener)<K extends 'abort'>(

    type: K,

    listener: (this: [AbortSignal](https://bun.com/reference/globals/AbortSignal), ev: AbortSignalEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
  + [throwIfAborted](https://bun.com/reference/globals/AbortSignal/throwIfAborted)(): void;
  + static [abort](https://bun.com/reference/globals/AbortSignal/abort)(

    reason?: any

    ): [AbortSignal](https://bun.com/reference/globals/AbortSignal);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/abort_static)
  + static [any](https://bun.com/reference/globals/AbortSignal/any)(

    signals: [AbortSignal](https://bun.com/reference/globals/AbortSignal)[]

    ): [AbortSignal](https://bun.com/reference/globals/AbortSignal);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/any_static)
  + static [timeout](https://bun.com/reference/globals/AbortSignal/timeout)(

    milliseconds: number

    ): [AbortSignal](https://bun.com/reference/globals/AbortSignal);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/AbortSignal/timeout_static)
* ### class [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)

  Represents a raw buffer of binary data, which is used to store data for the different typed arrays. ArrayBuffers cannot be read from or written to directly, but can be passed to a typed array or DataView Object to interpret the raw buffer as needed.

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/globals/ArrayBuffer/[toStringTag]): string
  + readonly [byteLength](https://bun.com/reference/globals/ArrayBuffer/byteLength): number

    Read-only. The length of the ArrayBuffer (in bytes).
  + [resize](https://bun.com/reference/globals/ArrayBuffer/resize)(

    newByteLength?: number

    ): void;

    Resizes the ArrayBuffer to the specified size (in bytes).

    [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/resize)

    [resize](https://bun.com/reference/globals/ArrayBuffer/resize)(

    byteLength: number

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    Resize an ArrayBuffer in-place.
  + [slice](https://bun.com/reference/globals/ArrayBuffer/slice)(

    begin: number,

    end?: number

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    Returns a section of an ArrayBuffer.
  + [transfer](https://bun.com/reference/globals/ArrayBuffer/transfer)(

    newByteLength?: number

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    Creates a new ArrayBuffer with the same byte content as this buffer, then detaches this buffer.

    [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/transfer)
  + [transferToFixedLength](https://bun.com/reference/globals/ArrayBuffer/transferToFixedLength)(

    newByteLength?: number

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    Creates a new non-resizable ArrayBuffer with the same byte content as this buffer, then detaches this buffer.

    [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/transferToFixedLength)
* ### class [Blob](https://bun.com/reference/globals/Blob)

  A file-like object of immutable, raw data. Blobs represent data that isn't necessarily in a JavaScript-native format. The File interface is based on Blob, inheriting blob functionality and expanding it to support files on the user's system.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob)

  + readonly [size](https://bun.com/reference/globals/Blob/size): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/size)
  + readonly [type](https://bun.com/reference/globals/Blob/type): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/type)
  + [arrayBuffer](https://bun.com/reference/globals/Blob/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns a promise that resolves to the contents of the blob as an ArrayBuffer
  + [bytes](https://bun.com/reference/globals/Blob/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/bytes)

    [bytes](https://bun.com/reference/globals/Blob/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a promise that resolves to the contents of the blob as a Uint8Array (array of bytes) its the same as `new Uint8Array(await blob.arrayBuffer())`
  + [formData](https://bun.com/reference/globals/Blob/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    Read the data from the blob as a FormData object.

    This first decodes the data from UTF-8, then parses it as a `multipart/form-data` body or a `application/x-www-form-urlencoded` body.

    The `type` property of the blob is used to determine the format of the body.

    This is a non-standard addition to the `Blob` API, to make it conform more closely to the `BodyMixin` API.
  + [json](https://bun.com/reference/globals/Blob/json)(): Promise<any>;

    Read the data from the blob as a JSON object.

    This first decodes the data from UTF-8, then parses it as JSON.
  + [slice](https://bun.com/reference/globals/Blob/slice)(

    start?: number,

    end?: number,

    contentType?: string

    ): [Blob](https://bun.com/reference/globals/Blob);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/slice)
  + [stream](https://bun.com/reference/globals/Blob/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/stream)

    [stream](https://bun.com/reference/globals/Blob/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a readable stream of the blob's contents
  + [text](https://bun.com/reference/globals/Blob/text)(): Promise<string>;

    Returns a promise that resolves to the contents of the blob as a string
* ### class [BroadcastChannel](https://bun.com/reference/globals/BroadcastChannel)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel)

  + readonly [name](https://bun.com/reference/globals/BroadcastChannel/name): string

    Returns the channel name (as passed to the constructor).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel/name)
  + [onmessage](https://bun.com/reference/globals/BroadcastChannel/onmessage): null | (this: [BroadcastChannel](https://bun.com/reference/globals/BroadcastChannel), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel/message_event)
  + [onmessageerror](https://bun.com/reference/globals/BroadcastChannel/onmessageerror): null | (this: [BroadcastChannel](https://bun.com/reference/globals/BroadcastChannel), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel/messageerror_event)
  + [addEventListener](https://bun.com/reference/globals/BroadcastChannel/addEventListener)<K extends keyof BroadcastChannelEventMap>(

    type: K,

    listener: (this: [BroadcastChannel](https://bun.com/reference/globals/BroadcastChannel), ev: BroadcastChannelEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/BroadcastChannel/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [close](https://bun.com/reference/globals/BroadcastChannel/close)(): void;

    Closes the BroadcastChannel object, opening it up to garbage collection.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel/close)
  + [dispatchEvent](https://bun.com/reference/globals/BroadcastChannel/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [postMessage](https://bun.com/reference/globals/BroadcastChannel/postMessage)(

    message: any

    ): void;

    Sends the given message to other BroadcastChannel objects set up for this channel. Messages can be structured objects, e.g. nested objects and arrays.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/BroadcastChannel/postMessage)
  + [removeEventListener](https://bun.com/reference/globals/BroadcastChannel/removeEventListener)<K extends keyof BroadcastChannelEventMap>(

    type: K,

    listener: (this: [BroadcastChannel](https://bun.com/reference/globals/BroadcastChannel), ev: BroadcastChannelEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/BroadcastChannel/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
* ### class [ByteLengthQueuingStrategy](https://bun.com/reference/globals/ByteLengthQueuingStrategy)

  This Streams API interface provides a built-in byte length queuing strategy that can be used when constructing streams.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ByteLengthQueuingStrategy)

  + readonly [highWaterMark](https://bun.com/reference/globals/ByteLengthQueuingStrategy/highWaterMark): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ByteLengthQueuingStrategy/highWaterMark)
  + readonly [size](https://bun.com/reference/globals/ByteLengthQueuingStrategy/size): [QueuingStrategySize](https://bun.com/reference/globals/QueuingStrategySize)<ArrayBufferView<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ByteLengthQueuingStrategy/size)
* ### class [CloseEvent](https://bun.com/reference/globals/CloseEvent)

  A CloseEvent is sent to clients using WebSockets when the connection is closed. This is delivered to the listener indicated by the WebSocket object's onclose attribute.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/CloseEvent)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/CloseEvent/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/CloseEvent/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/CloseEvent/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/CloseEvent/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/CloseEvent/CAPTURING_PHASE): 1
  + readonly [code](https://bun.com/reference/globals/CloseEvent/code): number

    Returns the WebSocket connection close code provided by the server.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CloseEvent/code)
  + readonly [composed](https://bun.com/reference/globals/CloseEvent/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/CloseEvent/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [defaultPrevented](https://bun.com/reference/globals/CloseEvent/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [eventPhase](https://bun.com/reference/globals/CloseEvent/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [isTrusted](https://bun.com/reference/globals/CloseEvent/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [NONE](https://bun.com/reference/globals/CloseEvent/NONE): 0
  + readonly [reason](https://bun.com/reference/globals/CloseEvent/reason): string

    Returns the WebSocket connection close reason provided by the server.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CloseEvent/reason)
  + readonly [target](https://bun.com/reference/globals/CloseEvent/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/CloseEvent/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/CloseEvent/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + readonly [wasClean](https://bun.com/reference/globals/CloseEvent/wasClean): boolean

    Returns true if the connection closed cleanly; false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CloseEvent/wasClean)
  + [composedPath](https://bun.com/reference/globals/CloseEvent/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/CloseEvent/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [stopImmediatePropagation](https://bun.com/reference/globals/CloseEvent/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/CloseEvent/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
* ### class [CompressionStream](https://bun.com/reference/globals/CompressionStream)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream)

  + readonly [readable](https://bun.com/reference/globals/CompressionStream/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/readable)
  + readonly [writable](https://bun.com/reference/globals/CompressionStream/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<BufferSource>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/writable)
* ### class [CountQueuingStrategy](https://bun.com/reference/globals/CountQueuingStrategy)

  This Streams API interface provides a built-in byte length queuing strategy that can be used when constructing streams.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/CountQueuingStrategy)

  + readonly [highWaterMark](https://bun.com/reference/globals/CountQueuingStrategy/highWaterMark): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CountQueuingStrategy/highWaterMark)
  + readonly [size](https://bun.com/reference/globals/CountQueuingStrategy/size): [QueuingStrategySize](https://bun.com/reference/globals/QueuingStrategySize)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CountQueuingStrategy/size)
* ### class [Crypto](https://bun.com/reference/globals/Crypto)

  Basic cryptography features available in the current context. It allows access to a cryptographically strong random number generator and to cryptographic primitives.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Crypto)

  + readonly [subtle](https://bun.com/reference/globals/Crypto/subtle): [SubtleCrypto](https://bun.com/reference/globals/SubtleCrypto)

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Crypto/subtle)
  + [timingSafeEqual](https://bun.com/reference/globals/Crypto/timingSafeEqual): (a: ArrayBufferView, b: ArrayBufferView) => boolean
  + [getRandomValues](https://bun.com/reference/globals/Crypto/getRandomValues)<T extends null | ArrayBufferView<ArrayBufferLike>>(

    array: T

    ): T;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Crypto/getRandomValues)
  + [randomUUID](https://bun.com/reference/globals/Crypto/randomUUID)(): `${string}-${string}-${string}-${string}-${string}`;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Crypto/randomUUID)
* ### class [CryptoKey](https://bun.com/reference/globals/CryptoKey)

  The CryptoKey dictionary of the Web Crypto API represents a cryptographic key. Available only in secure contexts.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/CryptoKey)

  + readonly [algorithm](https://bun.com/reference/globals/CryptoKey/algorithm): KeyAlgorithm

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CryptoKey/algorithm)
  + readonly [extractable](https://bun.com/reference/globals/CryptoKey/extractable): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CryptoKey/extractable)
  + readonly [type](https://bun.com/reference/globals/CryptoKey/type): KeyType

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CryptoKey/type)
  + readonly [usages](https://bun.com/reference/globals/CryptoKey/usages): KeyUsage[]

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CryptoKey/usages)
* ### class [CustomEvent](https://bun.com/reference/globals/CustomEvent)<T = any>

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/CustomEvent)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/CustomEvent/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/CustomEvent/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/CustomEvent/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/CustomEvent/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/CustomEvent/CAPTURING_PHASE): 1
  + readonly [composed](https://bun.com/reference/globals/CustomEvent/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/CustomEvent/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [defaultPrevented](https://bun.com/reference/globals/CustomEvent/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [detail](https://bun.com/reference/globals/CustomEvent/detail): T

    Returns any custom data event was created with. Typically used for synthetic events.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CustomEvent/detail)
  + readonly [eventPhase](https://bun.com/reference/globals/CustomEvent/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [isTrusted](https://bun.com/reference/globals/CustomEvent/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [NONE](https://bun.com/reference/globals/CustomEvent/NONE): 0
  + readonly [target](https://bun.com/reference/globals/CustomEvent/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/CustomEvent/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/CustomEvent/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + [composedPath](https://bun.com/reference/globals/CustomEvent/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/CustomEvent/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [stopImmediatePropagation](https://bun.com/reference/globals/CustomEvent/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/CustomEvent/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
* ### class [DecompressionStream](https://bun.com/reference/globals/DecompressionStream)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/DecompressionStream)

  + readonly [readable](https://bun.com/reference/globals/DecompressionStream/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/readable)
  + readonly [writable](https://bun.com/reference/globals/DecompressionStream/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<BufferSource>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/writable)
* ### class [DOMException](https://bun.com/reference/globals/DOMException)

  An abnormal event (called an exception) which occurs as a result of calling a method or accessing a property of a web API.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/DOMException)

  + readonly [ABORT\_ERR](https://bun.com/reference/globals/DOMException/ABORT_ERR): 20
  + [cause](https://bun.com/reference/globals/DOMException/cause)?: unknown

    The cause of the error.
  + readonly [DATA\_CLONE\_ERR](https://bun.com/reference/globals/DOMException/DATA_CLONE_ERR): 25
  + readonly [DOMSTRING\_SIZE\_ERR](https://bun.com/reference/globals/DOMException/DOMSTRING_SIZE_ERR): 2
  + readonly [HIERARCHY\_REQUEST\_ERR](https://bun.com/reference/globals/DOMException/HIERARCHY_REQUEST_ERR): 3
  + readonly [INDEX\_SIZE\_ERR](https://bun.com/reference/globals/DOMException/INDEX_SIZE_ERR): 1
  + readonly [INUSE\_ATTRIBUTE\_ERR](https://bun.com/reference/globals/DOMException/INUSE_ATTRIBUTE_ERR): 10
  + readonly [INVALID\_ACCESS\_ERR](https://bun.com/reference/globals/DOMException/INVALID_ACCESS_ERR): 15
  + readonly [INVALID\_CHARACTER\_ERR](https://bun.com/reference/globals/DOMException/INVALID_CHARACTER_ERR): 5
  + readonly [INVALID\_MODIFICATION\_ERR](https://bun.com/reference/globals/DOMException/INVALID_MODIFICATION_ERR): 13
  + readonly [INVALID\_NODE\_TYPE\_ERR](https://bun.com/reference/globals/DOMException/INVALID_NODE_TYPE_ERR): 24
  + readonly [INVALID\_STATE\_ERR](https://bun.com/reference/globals/DOMException/INVALID_STATE_ERR): 11
  + readonly [message](https://bun.com/reference/globals/DOMException/message): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DOMException/message)
  + readonly [name](https://bun.com/reference/globals/DOMException/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DOMException/name)
  + readonly [NAMESPACE\_ERR](https://bun.com/reference/globals/DOMException/NAMESPACE_ERR): 14
  + readonly [NETWORK\_ERR](https://bun.com/reference/globals/DOMException/NETWORK_ERR): 19
  + readonly [NO\_DATA\_ALLOWED\_ERR](https://bun.com/reference/globals/DOMException/NO_DATA_ALLOWED_ERR): 6
  + readonly [NO\_MODIFICATION\_ALLOWED\_ERR](https://bun.com/reference/globals/DOMException/NO_MODIFICATION_ALLOWED_ERR): 7
  + readonly [NOT\_FOUND\_ERR](https://bun.com/reference/globals/DOMException/NOT_FOUND_ERR): 8
  + readonly [NOT\_SUPPORTED\_ERR](https://bun.com/reference/globals/DOMException/NOT_SUPPORTED_ERR): 9
  + readonly [QUOTA\_EXCEEDED\_ERR](https://bun.com/reference/globals/DOMException/QUOTA_EXCEEDED_ERR): 22
  + readonly [SECURITY\_ERR](https://bun.com/reference/globals/DOMException/SECURITY_ERR): 18
  + [stack](https://bun.com/reference/globals/DOMException/stack)?: string
  + readonly [SYNTAX\_ERR](https://bun.com/reference/globals/DOMException/SYNTAX_ERR): 12
  + readonly [TIMEOUT\_ERR](https://bun.com/reference/globals/DOMException/TIMEOUT_ERR): 23
  + readonly [TYPE\_MISMATCH\_ERR](https://bun.com/reference/globals/DOMException/TYPE_MISMATCH_ERR): 17
  + readonly [URL\_MISMATCH\_ERR](https://bun.com/reference/globals/DOMException/URL_MISMATCH_ERR): 21
  + readonly [VALIDATION\_ERR](https://bun.com/reference/globals/DOMException/VALIDATION_ERR): 16
  + readonly [WRONG\_DOCUMENT\_ERR](https://bun.com/reference/globals/DOMException/WRONG_DOCUMENT_ERR): 4
  + readonly static [ABORT\_ERR](https://bun.com/reference/globals/DOMException/ABORT_ERR): 20
  + readonly static [DATA\_CLONE\_ERR](https://bun.com/reference/globals/DOMException/DATA_CLONE_ERR): 25
  + readonly static [DOMSTRING\_SIZE\_ERR](https://bun.com/reference/globals/DOMException/DOMSTRING_SIZE_ERR): 2
  + readonly static [HIERARCHY\_REQUEST\_ERR](https://bun.com/reference/globals/DOMException/HIERARCHY_REQUEST_ERR): 3
  + readonly static [INDEX\_SIZE\_ERR](https://bun.com/reference/globals/DOMException/INDEX_SIZE_ERR): 1
  + readonly static [INUSE\_ATTRIBUTE\_ERR](https://bun.com/reference/globals/DOMException/INUSE_ATTRIBUTE_ERR): 10
  + readonly static [INVALID\_ACCESS\_ERR](https://bun.com/reference/globals/DOMException/INVALID_ACCESS_ERR): 15
  + readonly static [INVALID\_CHARACTER\_ERR](https://bun.com/reference/globals/DOMException/INVALID_CHARACTER_ERR): 5
  + readonly static [INVALID\_MODIFICATION\_ERR](https://bun.com/reference/globals/DOMException/INVALID_MODIFICATION_ERR): 13
  + readonly static [INVALID\_NODE\_TYPE\_ERR](https://bun.com/reference/globals/DOMException/INVALID_NODE_TYPE_ERR): 24
  + readonly static [INVALID\_STATE\_ERR](https://bun.com/reference/globals/DOMException/INVALID_STATE_ERR): 11
  + readonly static [NAMESPACE\_ERR](https://bun.com/reference/globals/DOMException/NAMESPACE_ERR): 14
  + readonly static [NETWORK\_ERR](https://bun.com/reference/globals/DOMException/NETWORK_ERR): 19
  + readonly static [NO\_DATA\_ALLOWED\_ERR](https://bun.com/reference/globals/DOMException/NO_DATA_ALLOWED_ERR): 6
  + readonly static [NO\_MODIFICATION\_ALLOWED\_ERR](https://bun.com/reference/globals/DOMException/NO_MODIFICATION_ALLOWED_ERR): 7
  + readonly static [NOT\_FOUND\_ERR](https://bun.com/reference/globals/DOMException/NOT_FOUND_ERR): 8
  + readonly static [NOT\_SUPPORTED\_ERR](https://bun.com/reference/globals/DOMException/NOT_SUPPORTED_ERR): 9
  + readonly static [QUOTA\_EXCEEDED\_ERR](https://bun.com/reference/globals/DOMException/QUOTA_EXCEEDED_ERR): 22
  + readonly static [SECURITY\_ERR](https://bun.com/reference/globals/DOMException/SECURITY_ERR): 18
  + readonly static [SYNTAX\_ERR](https://bun.com/reference/globals/DOMException/SYNTAX_ERR): 12
  + readonly static [TIMEOUT\_ERR](https://bun.com/reference/globals/DOMException/TIMEOUT_ERR): 23
  + readonly static [TYPE\_MISMATCH\_ERR](https://bun.com/reference/globals/DOMException/TYPE_MISMATCH_ERR): 17
  + readonly static [URL\_MISMATCH\_ERR](https://bun.com/reference/globals/DOMException/URL_MISMATCH_ERR): 21
  + readonly static [VALIDATION\_ERR](https://bun.com/reference/globals/DOMException/VALIDATION_ERR): 16
  + readonly static [WRONG\_DOCUMENT\_ERR](https://bun.com/reference/globals/DOMException/WRONG_DOCUMENT_ERR): 4
* ### class [ErrorEvent](https://bun.com/reference/globals/ErrorEvent)

  Events providing information related to errors in scripts or in files.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/ErrorEvent/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/ErrorEvent/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/ErrorEvent/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/ErrorEvent/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/ErrorEvent/CAPTURING_PHASE): 1
  + readonly [colno](https://bun.com/reference/globals/ErrorEvent/colno): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent/colno)
  + readonly [composed](https://bun.com/reference/globals/ErrorEvent/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/ErrorEvent/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [defaultPrevented](https://bun.com/reference/globals/ErrorEvent/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [error](https://bun.com/reference/globals/ErrorEvent/error): any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent/error)
  + readonly [eventPhase](https://bun.com/reference/globals/ErrorEvent/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [filename](https://bun.com/reference/globals/ErrorEvent/filename): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent/filename)
  + readonly [isTrusted](https://bun.com/reference/globals/ErrorEvent/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [lineno](https://bun.com/reference/globals/ErrorEvent/lineno): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent/lineno)
  + readonly [message](https://bun.com/reference/globals/ErrorEvent/message): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ErrorEvent/message)
  + readonly [NONE](https://bun.com/reference/globals/ErrorEvent/NONE): 0
  + readonly [target](https://bun.com/reference/globals/ErrorEvent/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/ErrorEvent/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/ErrorEvent/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + [composedPath](https://bun.com/reference/globals/ErrorEvent/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/ErrorEvent/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [stopImmediatePropagation](https://bun.com/reference/globals/ErrorEvent/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/ErrorEvent/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
* ### class [Event](https://bun.com/reference/globals/Event)

  An event which takes place in the DOM.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/Event/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/Event/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/Event/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/Event/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/Event/CAPTURING_PHASE): 1
  + readonly [composed](https://bun.com/reference/globals/Event/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/Event/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [defaultPrevented](https://bun.com/reference/globals/Event/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [eventPhase](https://bun.com/reference/globals/Event/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [isTrusted](https://bun.com/reference/globals/Event/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [NONE](https://bun.com/reference/globals/Event/NONE): 0
  + readonly [target](https://bun.com/reference/globals/Event/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/Event/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/Event/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + readonly static [AT\_TARGET](https://bun.com/reference/globals/Event/AT_TARGET): 2
  + readonly static [BUBBLING\_PHASE](https://bun.com/reference/globals/Event/BUBBLING_PHASE): 3
  + readonly static [CAPTURING\_PHASE](https://bun.com/reference/globals/Event/CAPTURING_PHASE): 1
  + readonly static [NONE](https://bun.com/reference/globals/Event/NONE): 0
  + [composedPath](https://bun.com/reference/globals/Event/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/Event/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [stopImmediatePropagation](https://bun.com/reference/globals/Event/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/Event/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
* ### class [EventTarget](https://bun.com/reference/globals/EventTarget)

  EventTarget is a DOM interface implemented by objects that can receive events and may have listeners for them.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget)

  + [addEventListener](https://bun.com/reference/globals/EventTarget/addEventListener)(

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

    [addEventListener](https://bun.com/reference/globals/EventTarget/addEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

    ): void;

    Adds a new handler for the `type` event. Any given `listener` is added only once per `type` and per `capture` option value.

    If the `once` option is true, the `listener` is removed after the next time a `type` event is dispatched.

    The `capture` option is not used by Node.js in any functional way other than tracking registered event listeners per the `EventTarget` specification. Specifically, the `capture` option is used as part of the key when registering a `listener`. Any individual `listener` may be added once with `capture = false`, and once with `capture = true`.
  + [dispatchEvent](https://bun.com/reference/globals/EventTarget/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [removeEventListener](https://bun.com/reference/globals/EventTarget/removeEventListener)(

    type: string,

    callback: null | EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/EventTarget/removeEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [EventListenerOptions](https://bun.com/reference/bun/EventListenerOptions)

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.
* ### class [File](https://bun.com/reference/globals/File)

  Provides information about files and allows JavaScript in a web page to access their content.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/File)

  + readonly [lastModified](https://bun.com/reference/globals/File/lastModified): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/File/lastModified)
  + readonly [name](https://bun.com/reference/globals/File/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/File/name)
  + readonly [size](https://bun.com/reference/globals/File/size): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/size)
  + readonly [type](https://bun.com/reference/globals/File/type): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/type)
  + readonly [webkitRelativePath](https://bun.com/reference/globals/File/webkitRelativePath): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/File/webkitRelativePath)
  + [arrayBuffer](https://bun.com/reference/globals/File/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns a promise that resolves to the contents of the blob as an ArrayBuffer
  + [bytes](https://bun.com/reference/globals/File/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/bytes)

    [bytes](https://bun.com/reference/globals/File/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a promise that resolves to the contents of the blob as a Uint8Array (array of bytes) its the same as `new Uint8Array(await blob.arrayBuffer())`
  + [formData](https://bun.com/reference/globals/File/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    Read the data from the blob as a FormData object.

    This first decodes the data from UTF-8, then parses it as a `multipart/form-data` body or a `application/x-www-form-urlencoded` body.

    The `type` property of the blob is used to determine the format of the body.

    This is a non-standard addition to the `Blob` API, to make it conform more closely to the `BodyMixin` API.
  + [json](https://bun.com/reference/globals/File/json)(): Promise<any>;

    Read the data from the blob as a JSON object.

    This first decodes the data from UTF-8, then parses it as JSON.
  + [slice](https://bun.com/reference/globals/File/slice)(

    start?: number,

    end?: number,

    contentType?: string

    ): [Blob](https://bun.com/reference/globals/Blob);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/slice)
  + [stream](https://bun.com/reference/globals/File/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Blob/stream)

    [stream](https://bun.com/reference/globals/File/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a readable stream of the blob's contents
  + [text](https://bun.com/reference/globals/File/text)(): Promise<string>;

    Returns a promise that resolves to the contents of the blob as a string
* ### class [FormData](https://bun.com/reference/globals/FormData)

  Provides a way to easily construct a set of key/value pairs representing form fields and their values, which can then be easily sent using the XMLHttpRequest.send() method. It uses the same format a form would use if the encoding type were set to "multipart/form-data".

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData)

  + [[Symbol.iterator]](https://bun.com/reference/globals/FormData/[iterator])(): FormDataIterator<[string, FormDataEntryValue]>;
  + [append](https://bun.com/reference/globals/FormData/append)(

    name: string,

    value: string | [Blob](https://bun.com/reference/globals/Blob)

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/append)

    [append](https://bun.com/reference/globals/FormData/append)(

    name: string,

    value: string

    ): void;

    [append](https://bun.com/reference/globals/FormData/append)(

    name: string,

    blobValue: [Blob](https://bun.com/reference/globals/Blob),

    filename?: string

    ): void;
  + [delete](https://bun.com/reference/globals/FormData/delete)(

    name: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/delete)
  + [entries](https://bun.com/reference/globals/FormData/entries)(): FormDataIterator<[string, FormDataEntryValue]>;

    Returns an array of key, value pairs for every entry in the list.

    [entries](https://bun.com/reference/globals/FormData/entries)(): IterableIterator<[string, string]>;
  + [forEach](https://bun.com/reference/globals/FormData/forEach)(

    callbackfn: (value: [FormDataEntryValue](https://bun.com/reference/bun/FormDataEntryValue), key: string, parent: [FormData](https://bun.com/reference/globals/FormData)) => void,

    thisArg?: any

    ): void;
  + [get](https://bun.com/reference/globals/FormData/get)(

    name: string

    ): null | [FormDataEntryValue](https://bun.com/reference/bun/FormDataEntryValue);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/get)
  + [getAll](https://bun.com/reference/globals/FormData/getAll)(

    name: string

    ): [FormDataEntryValue](https://bun.com/reference/bun/FormDataEntryValue)[];

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/getAll)
  + [has](https://bun.com/reference/globals/FormData/has)(

    name: string

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/has)
  + [keys](https://bun.com/reference/globals/FormData/keys)(): FormDataIterator<string>;

    Returns a list of keys in the list.

    [keys](https://bun.com/reference/globals/FormData/keys)(): IterableIterator<string>;
  + [set](https://bun.com/reference/globals/FormData/set)(

    name: string,

    value: string | [Blob](https://bun.com/reference/globals/Blob)

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/FormData/set)

    [set](https://bun.com/reference/globals/FormData/set)(

    name: string,

    value: string

    ): void;

    [set](https://bun.com/reference/globals/FormData/set)(

    name: string,

    blobValue: [Blob](https://bun.com/reference/globals/Blob),

    filename?: string

    ): void;
  + [values](https://bun.com/reference/globals/FormData/values)(): FormDataIterator<FormDataEntryValue>;

    Returns a list of values in the list.

    [values](https://bun.com/reference/globals/FormData/values)(): IterableIterator<string>;
* ### class [Headers](https://bun.com/reference/globals/Headers)

  This Fetch API interface allows you to perform various actions on HTTP request and response headers. These actions include retrieving, setting, adding to, and removing. A Headers object has an associated header list, which is initially empty and consists of zero or more name and value pairs.  You can add to this using methods like append() (see Examples.) In all methods of this interface, header names are matched by case-insensitive byte sequence.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers)

  + readonly [count](https://bun.com/reference/globals/Headers/count): number

    Get the total number of headers
  + [[Symbol.iterator]](https://bun.com/reference/globals/Headers/[iterator])(): HeadersIterator<[string, string]>;
  + [append](https://bun.com/reference/globals/Headers/append)(

    name: string,

    value: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/append)
  + [delete](https://bun.com/reference/globals/Headers/delete)(

    name: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/delete)
  + [entries](https://bun.com/reference/globals/Headers/entries)(): HeadersIterator<[string, string]>;

    Returns an iterator allowing to go through all key/value pairs contained in this object.
  + [forEach](https://bun.com/reference/globals/Headers/forEach)(

    callbackfn: (value: string, key: string, parent: [Headers](https://bun.com/reference/globals/Headers)) => void,

    thisArg?: any

    ): void;
  + [get](https://bun.com/reference/globals/Headers/get)(

    name: string

    ): null | string;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/get)
  + [getAll](https://bun.com/reference/globals/Headers/getAll)(

    name: 'set-cookie' | 'Set-Cookie'

    ): string[];

    Get all headers matching the name

    Only supports `"Set-Cookie"`. All other headers are empty arrays.

    @param name

    The header name to get

    @returns

    An array of header values

    ```
    const headers = new Headers();
    headers.append("Set-Cookie", "foo=bar");
    headers.append("Set-Cookie", "baz=qux");
    headers.getAll("Set-Cookie"); // ["foo=bar", "baz=qux"]
    ```
  + [getSetCookie](https://bun.com/reference/globals/Headers/getSetCookie)(): string[];

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/getSetCookie)
  + [has](https://bun.com/reference/globals/Headers/has)(

    name: string

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/has)
  + [keys](https://bun.com/reference/globals/Headers/keys)(): HeadersIterator<string>;

    Returns an iterator allowing to go through all keys of the key/value pairs contained in this object.
  + [set](https://bun.com/reference/globals/Headers/set)(

    name: string,

    value: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Headers/set)
  + [toJSON](https://bun.com/reference/globals/Headers/toJSON)(): Record<string, string> & { set-cookie: string[] };

    Convert Headers to a plain JavaScript object.

    About 10x faster than `Object.fromEntries(headers.entries())`

    Called when you run `JSON.stringify(headers)`

    Does not preserve insertion order. Well-known header names are lowercased. Other header names are left as-is.
  + [values](https://bun.com/reference/globals/Headers/values)(): HeadersIterator<string>;

    Returns an iterator allowing to go through all values of the key/value pairs contained in this object.
* ### class [MessageChannel](https://bun.com/reference/globals/MessageChannel)

  This Channel Messaging API interface allows us to create a new message channel and send data through it via its two MessagePort properties.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageChannel)

  + readonly [port1](https://bun.com/reference/globals/MessageChannel/port1): [MessagePort](https://bun.com/reference/globals/MessagePort)

    Returns the first MessagePort object.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageChannel/port1)
  + readonly [port2](https://bun.com/reference/globals/MessageChannel/port2): [MessagePort](https://bun.com/reference/globals/MessagePort)

    Returns the second MessagePort object.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessageChannel/port2)
* ### class [MessagePort](https://bun.com/reference/globals/MessagePort)

  This Channel Messaging API interface represents one of the two ports of a MessageChannel, allowing messages to be sent from one port and listening out for them arriving at the other.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessagePort)

  + [onmessage](https://bun.com/reference/globals/MessagePort/onmessage): null | (this: [MessagePort](https://bun.com/reference/globals/MessagePort), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DedicatedWorkerGlobalScope/message_event)
  + [onmessageerror](https://bun.com/reference/globals/MessagePort/onmessageerror): null | (this: [MessagePort](https://bun.com/reference/globals/MessagePort), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DedicatedWorkerGlobalScope/messageerror_event)
  + [addEventListener](https://bun.com/reference/globals/MessagePort/addEventListener)<K extends keyof MessagePortEventMap>(

    type: K,

    listener: (this: [MessagePort](https://bun.com/reference/globals/MessagePort), ev: MessagePortEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/MessagePort/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [close](https://bun.com/reference/globals/MessagePort/close)(): void;

    Disconnects the port, so that it is no longer active.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessagePort/close)
  + [dispatchEvent](https://bun.com/reference/globals/MessagePort/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [postMessage](https://bun.com/reference/globals/MessagePort/postMessage)(

    message: any,

    transfer: Transferable[]

    ): void;

    Posts a message through the channel. Objects listed in transfer are transferred, not just cloned, meaning that they are no longer usable on the sending side.

    Throws a "DataCloneError" DOMException if transfer contains duplicate objects or port, or if message could not be cloned.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessagePort/postMessage)

    [postMessage](https://bun.com/reference/globals/MessagePort/postMessage)(

    message: any,

    options?: StructuredSerializeOptions

    ): void;
  + [removeEventListener](https://bun.com/reference/globals/MessagePort/removeEventListener)<K extends keyof MessagePortEventMap>(

    type: K,

    listener: (this: [MessagePort](https://bun.com/reference/globals/MessagePort), ev: MessagePortEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/MessagePort/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
  + [start](https://bun.com/reference/globals/MessagePort/start)(): void;

    Begins dispatching messages received on the port.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/MessagePort/start)
* ### class [Navigator](https://bun.com/reference/globals/Navigator)

  The state and the identity of the user agent. It allows scripts to query it and to register themselves to carry on some activities.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator)

  + readonly [clipboard](https://bun.com/reference/globals/Navigator/clipboard): Clipboard

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/clipboard)
  + readonly [cookieEnabled](https://bun.com/reference/globals/Navigator/cookieEnabled): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/cookieEnabled)
  + readonly [credentials](https://bun.com/reference/globals/Navigator/credentials): CredentialsContainer

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/credentials)
  + readonly [doNotTrack](https://bun.com/reference/globals/Navigator/doNotTrack): null | string
  + readonly [geolocation](https://bun.com/reference/globals/Navigator/geolocation): Geolocation

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/geolocation)
  + readonly [hardwareConcurrency](https://bun.com/reference/globals/Navigator/hardwareConcurrency): number
  + readonly [language](https://bun.com/reference/globals/Navigator/language): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/language)
  + readonly [languages](https://bun.com/reference/globals/Navigator/languages): readonly string[]

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/languages)
  + readonly [locks](https://bun.com/reference/globals/Navigator/locks): LockManager

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/locks)
  + readonly [maxTouchPoints](https://bun.com/reference/globals/Navigator/maxTouchPoints): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/maxTouchPoints)
  + readonly [mediaCapabilities](https://bun.com/reference/globals/Navigator/mediaCapabilities): MediaCapabilities

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/mediaCapabilities)
  + readonly [mediaDevices](https://bun.com/reference/globals/Navigator/mediaDevices): MediaDevices

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/mediaDevices)
  + readonly [mediaSession](https://bun.com/reference/globals/Navigator/mediaSession): MediaSession

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/mediaSession)
  + readonly [onLine](https://bun.com/reference/globals/Navigator/onLine): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/onLine)
  + readonly [pdfViewerEnabled](https://bun.com/reference/globals/Navigator/pdfViewerEnabled): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/pdfViewerEnabled)
  + readonly [permissions](https://bun.com/reference/globals/Navigator/permissions): Permissions

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/permissions)
  + readonly [platform](https://bun.com/reference/globals/Navigator/platform): 'MacIntel' | 'Win32' | 'Linux x86\_64'
  + readonly [serviceWorker](https://bun.com/reference/globals/Navigator/serviceWorker): ServiceWorkerContainer

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/serviceWorker)
  + readonly [storage](https://bun.com/reference/globals/Navigator/storage): StorageManager

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/storage)
  + readonly [userActivation](https://bun.com/reference/globals/Navigator/userActivation): UserActivation

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/userActivation)
  + readonly [userAgent](https://bun.com/reference/globals/Navigator/userAgent): string
  + readonly [wakeLock](https://bun.com/reference/globals/Navigator/wakeLock): WakeLock

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/wakeLock)
  + readonly [webdriver](https://bun.com/reference/globals/Navigator/webdriver): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/webdriver)
  + [canShare](https://bun.com/reference/globals/Navigator/canShare)(

    data?: ShareData

    ): boolean;

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/canShare)
  + [clearAppBadge](https://bun.com/reference/globals/Navigator/clearAppBadge)(): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/clearAppBadge)
  + [getGamepads](https://bun.com/reference/globals/Navigator/getGamepads)(): null | Gamepad[];

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/getGamepads)

  + [requestMediaKeySystemAccess](https://bun.com/reference/globals/Navigator/requestMediaKeySystemAccess)(

    keySystem: string,

    supportedConfigurations: MediaKeySystemConfiguration[]

    ): Promise<MediaKeySystemAccess>;

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/requestMediaKeySystemAccess)

    [requestMediaKeySystemAccess](https://bun.com/reference/globals/Navigator/requestMediaKeySystemAccess)(

    keySystem: string,

    supportedConfigurations: Iterable<MediaKeySystemConfiguration>

    ): Promise<MediaKeySystemAccess>;

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/requestMediaKeySystemAccess)
  + [requestMIDIAccess](https://bun.com/reference/globals/Navigator/requestMIDIAccess)(

    options?: MIDIOptions

    ): Promise<MIDIAccess>;

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/requestMIDIAccess)
  + [sendBeacon](https://bun.com/reference/globals/Navigator/sendBeacon)(

    url: string | [URL](https://bun.com/reference/globals/URL),

    data?: null | BodyInit

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/sendBeacon)
  + [setAppBadge](https://bun.com/reference/globals/Navigator/setAppBadge)(

    contents?: number

    ): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/setAppBadge)
  + [share](https://bun.com/reference/globals/Navigator/share)(

    data?: ShareData

    ): Promise<void>;

    Available only in secure contexts.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/share)
  + [vibrate](https://bun.com/reference/globals/Navigator/vibrate)(

    pattern: VibratePattern

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/vibrate)

    [vibrate](https://bun.com/reference/globals/Navigator/vibrate)(

    pattern: Iterable<number>

    ): boolean;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Navigator/vibrate)
* ### class [Performance](https://bun.com/reference/globals/Performance)

  Provides access to performance-related information for the current page. It's part of the High Resolution Time API, but is enhanced by the Performance Timeline API, the Navigation Timing API, the User Timing API, and the Resource Timing API.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance)

  + readonly [eventCounts](https://bun.com/reference/globals/Performance/eventCounts): EventCounts

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/eventCounts)
  + [onresourcetimingbufferfull](https://bun.com/reference/globals/Performance/onresourcetimingbufferfull): null | (this: [Performance](https://bun.com/reference/globals/Performance), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/resourcetimingbufferfull_event)
  + readonly [timeOrigin](https://bun.com/reference/globals/Performance/timeOrigin): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/timeOrigin)
  + [addEventListener](https://bun.com/reference/globals/Performance/addEventListener)<K extends 'resourcetimingbufferfull'>(

    type: K,

    listener: (this: [Performance](https://bun.com/reference/globals/Performance), ev: PerformanceEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/Performance/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [clearMarks](https://bun.com/reference/globals/Performance/clearMarks)(

    markName?: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/clearMarks)
  + [clearMeasures](https://bun.com/reference/globals/Performance/clearMeasures)(

    measureName?: string

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/clearMeasures)
  + [clearResourceTimings](https://bun.com/reference/globals/Performance/clearResourceTimings)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/clearResourceTimings)
  + [dispatchEvent](https://bun.com/reference/globals/Performance/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [getEntries](https://bun.com/reference/globals/Performance/getEntries)(): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/getEntries)
  + [getEntriesByName](https://bun.com/reference/globals/Performance/getEntriesByName)(

    name: string,

    type?: string

    ): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/getEntriesByName)
  + [getEntriesByType](https://bun.com/reference/globals/Performance/getEntriesByType)(

    type: string

    ): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/getEntriesByType)
  + [mark](https://bun.com/reference/globals/Performance/mark)(

    markName: string,

    markOptions?: PerformanceMarkOptions

    ): [PerformanceMark](https://bun.com/reference/globals/PerformanceMark);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/mark)
  + [measure](https://bun.com/reference/globals/Performance/measure)(

    measureName: string,

    startOrMeasureOptions?: string | PerformanceMeasureOptions,

    endMark?: string

    ): [PerformanceMeasure](https://bun.com/reference/globals/PerformanceMeasure);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/measure)
  + [now](https://bun.com/reference/globals/Performance/now)(): number;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/now)
  + [removeEventListener](https://bun.com/reference/globals/Performance/removeEventListener)<K extends 'resourcetimingbufferfull'>(

    type: K,

    listener: (this: [Performance](https://bun.com/reference/globals/Performance), ev: PerformanceEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/Performance/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
  + [setResourceTimingBufferSize](https://bun.com/reference/globals/Performance/setResourceTimingBufferSize)(

    maxSize: number

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/setResourceTimingBufferSize)
  + [toJSON](https://bun.com/reference/globals/Performance/toJSON)(): any;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Performance/toJSON)
* ### class [PerformanceEntry](https://bun.com/reference/globals/PerformanceEntry)

  Encapsulates a single performance metric that is part of the performance timeline. A performance entry can be directly created by making a performance mark or measure (for example by calling the mark() method) at an explicit point in an application. Performance entries are also created in indirect ways such as loading a resource (such as an image).

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry)

  + readonly [duration](https://bun.com/reference/globals/PerformanceEntry/duration): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/duration)
  + readonly [entryType](https://bun.com/reference/globals/PerformanceEntry/entryType): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/entryType)
  + readonly [name](https://bun.com/reference/globals/PerformanceEntry/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/name)
  + readonly [startTime](https://bun.com/reference/globals/PerformanceEntry/startTime): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/startTime)
  + [toJSON](https://bun.com/reference/globals/PerformanceEntry/toJSON)(): any;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/toJSON)
* ### class [PerformanceMark](https://bun.com/reference/globals/PerformanceMark)

  PerformanceMark is an abstract interface for PerformanceEntry objects with an entryType of "mark". Entries of this type are created by calling performance.mark() to add a named DOMHighResTimeStamp (the mark) to the browser's performance timeline.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceMark)

  + readonly [detail](https://bun.com/reference/globals/PerformanceMark/detail): any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceMark/detail)
  + readonly [duration](https://bun.com/reference/globals/PerformanceMark/duration): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/duration)
  + readonly [entryType](https://bun.com/reference/globals/PerformanceMark/entryType): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/entryType)
  + readonly [name](https://bun.com/reference/globals/PerformanceMark/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/name)
  + readonly [startTime](https://bun.com/reference/globals/PerformanceMark/startTime): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/startTime)
  + [toJSON](https://bun.com/reference/globals/PerformanceMark/toJSON)(): any;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/toJSON)
* ### class [PerformanceMeasure](https://bun.com/reference/globals/PerformanceMeasure)

  PerformanceMeasure is an abstract interface for PerformanceEntry objects with an entryType of "measure". Entries of this type are created by calling performance.measure() to add a named DOMHighResTimeStamp (the measure) between two marks to the browser's performance timeline.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceMeasure)

  + readonly [detail](https://bun.com/reference/globals/PerformanceMeasure/detail): any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceMeasure/detail)
  + readonly [duration](https://bun.com/reference/globals/PerformanceMeasure/duration): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/duration)
  + readonly [entryType](https://bun.com/reference/globals/PerformanceMeasure/entryType): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/entryType)
  + readonly [name](https://bun.com/reference/globals/PerformanceMeasure/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/name)
  + readonly [startTime](https://bun.com/reference/globals/PerformanceMeasure/startTime): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/startTime)
  + [toJSON](https://bun.com/reference/globals/PerformanceMeasure/toJSON)(): any;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/toJSON)
* ### class [PerformanceObserver](https://bun.com/reference/globals/PerformanceObserver)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserver)

  + readonly static [supportedEntryTypes](https://bun.com/reference/globals/PerformanceObserver/supportedEntryTypes): readonly string[]

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/supportedEntryTypes_static)
  + [disconnect](https://bun.com/reference/globals/PerformanceObserver/disconnect)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/disconnect)
  + [observe](https://bun.com/reference/globals/PerformanceObserver/observe)(

    options?: PerformanceObserverInit

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/observe)
  + [takeRecords](https://bun.com/reference/globals/PerformanceObserver/takeRecords)(): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/takeRecords)
* ### class [PerformanceObserverEntryList](https://bun.com/reference/globals/PerformanceObserverEntryList)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserverEntryList)

  + [getEntries](https://bun.com/reference/globals/PerformanceObserverEntryList/getEntries)(): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserverEntryList/getEntries)
  + [getEntriesByName](https://bun.com/reference/globals/PerformanceObserverEntryList/getEntriesByName)(

    name: string,

    type?: string

    ): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserverEntryList/getEntriesByName)
  + [getEntriesByType](https://bun.com/reference/globals/PerformanceObserverEntryList/getEntriesByType)(

    type: string

    ): PerformanceEntryList;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceObserverEntryList/getEntriesByType)
* ### class [PerformanceResourceTiming](https://bun.com/reference/globals/PerformanceResourceTiming)

  Enables retrieval and analysis of detailed network timing data regarding the loading of an application's resources. An application can use the timing metrics to determine, for example, the length of time it takes to fetch a specific resource, such as an XMLHttpRequest, <SVG>, image, or script.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming)

  + readonly [connectEnd](https://bun.com/reference/globals/PerformanceResourceTiming/connectEnd): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/connectEnd)
  + readonly [connectStart](https://bun.com/reference/globals/PerformanceResourceTiming/connectStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/connectStart)
  + readonly [decodedBodySize](https://bun.com/reference/globals/PerformanceResourceTiming/decodedBodySize): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/decodedBodySize)
  + readonly [domainLookupEnd](https://bun.com/reference/globals/PerformanceResourceTiming/domainLookupEnd): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/domainLookupEnd)
  + readonly [domainLookupStart](https://bun.com/reference/globals/PerformanceResourceTiming/domainLookupStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/domainLookupStart)
  + readonly [duration](https://bun.com/reference/globals/PerformanceResourceTiming/duration): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/duration)
  + readonly [encodedBodySize](https://bun.com/reference/globals/PerformanceResourceTiming/encodedBodySize): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/encodedBodySize)
  + readonly [entryType](https://bun.com/reference/globals/PerformanceResourceTiming/entryType): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/entryType)
  + readonly [fetchStart](https://bun.com/reference/globals/PerformanceResourceTiming/fetchStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/fetchStart)
  + readonly [initiatorType](https://bun.com/reference/globals/PerformanceResourceTiming/initiatorType): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/initiatorType)
  + readonly [name](https://bun.com/reference/globals/PerformanceResourceTiming/name): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/name)
  + readonly [redirectEnd](https://bun.com/reference/globals/PerformanceResourceTiming/redirectEnd): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/redirectEnd)
  + readonly [redirectStart](https://bun.com/reference/globals/PerformanceResourceTiming/redirectStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/redirectStart)
  + readonly [requestStart](https://bun.com/reference/globals/PerformanceResourceTiming/requestStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/requestStart)
  + readonly [responseEnd](https://bun.com/reference/globals/PerformanceResourceTiming/responseEnd): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/responseEnd)
  + readonly [responseStart](https://bun.com/reference/globals/PerformanceResourceTiming/responseStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/responseStart)
  + readonly [responseStatus](https://bun.com/reference/globals/PerformanceResourceTiming/responseStatus): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/responseStatus)
  + readonly [secureConnectionStart](https://bun.com/reference/globals/PerformanceResourceTiming/secureConnectionStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/secureConnectionStart)
  + readonly [serverTiming](https://bun.com/reference/globals/PerformanceResourceTiming/serverTiming): readonly PerformanceServerTiming[]

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/serverTiming)
  + readonly [startTime](https://bun.com/reference/globals/PerformanceResourceTiming/startTime): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceEntry/startTime)
  + readonly [transferSize](https://bun.com/reference/globals/PerformanceResourceTiming/transferSize): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/transferSize)
  + readonly [workerStart](https://bun.com/reference/globals/PerformanceResourceTiming/workerStart): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/workerStart)
  + [toJSON](https://bun.com/reference/globals/PerformanceResourceTiming/toJSON)(): any;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming/toJSON)
* ### class [ReadableByteStreamController](https://bun.com/reference/globals/ReadableByteStreamController)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController)

  + readonly [byobRequest](https://bun.com/reference/globals/ReadableByteStreamController/byobRequest): null | [ReadableStreamBYOBRequest](https://bun.com/reference/globals/ReadableStreamBYOBRequest)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController/byobRequest)
  + readonly [desiredSize](https://bun.com/reference/globals/ReadableByteStreamController/desiredSize): null | number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController/desiredSize)
  + [close](https://bun.com/reference/globals/ReadableByteStreamController/close)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController/close)
  + [enqueue](https://bun.com/reference/globals/ReadableByteStreamController/enqueue)(

    chunk: ArrayBufferView

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController/enqueue)
  + [error](https://bun.com/reference/globals/ReadableByteStreamController/error)(

    e?: any

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableByteStreamController/error)
* ### class [ReadableStream](https://bun.com/reference/globals/ReadableStream)<R = any>

  This Streams API interface represents a readable stream of byte data. The Fetch API offers a concrete instance of a ReadableStream through the body property of a Response object.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream)

  + readonly [locked](https://bun.com/reference/globals/ReadableStream/locked): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/locked)
  + [[Symbol.asyncIterator]](https://bun.com/reference/globals/ReadableStream/[asyncIterator])(

    options?: ReadableStreamIteratorOptions

    ): ReadableStreamAsyncIterator<R>;
  + [cancel](https://bun.com/reference/globals/ReadableStream/cancel)(

    reason?: any

    ): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/cancel)
  + [getReader](https://bun.com/reference/globals/ReadableStream/getReader)(

    options: { mode: 'byob' }

    ): [ReadableStreamBYOBReader](https://bun.com/reference/globals/ReadableStreamBYOBReader);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/getReader)

    [getReader](https://bun.com/reference/globals/ReadableStream/getReader)(): [ReadableStreamDefaultReader](https://bun.com/reference/globals/ReadableStreamDefaultReader)<R>;

    [getReader](https://bun.com/reference/globals/ReadableStream/getReader)(

    options?: ReadableStreamGetReaderOptions

    ): ReadableStreamReader<R>;
  + [pipeThrough](https://bun.com/reference/globals/ReadableStream/pipeThrough)<T>(

    transform: [ReadableWritablePair](https://bun.com/reference/globals/ReadableWritablePair)<T, R>,

    options?: [StreamPipeOptions](https://bun.com/reference/globals/StreamPipeOptions)

    ): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<T>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/pipeThrough)
  + [pipeTo](https://bun.com/reference/globals/ReadableStream/pipeTo)(

    destination: [WritableStream](https://bun.com/reference/globals/WritableStream)<R>,

    options?: [StreamPipeOptions](https://bun.com/reference/globals/StreamPipeOptions)

    ): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/pipeTo)
  + [tee](https://bun.com/reference/globals/ReadableStream/tee)(): [[ReadableStream](https://bun.com/reference/globals/ReadableStream)<R>, [ReadableStream](https://bun.com/reference/globals/ReadableStream)<R>];

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStream/tee)
  + [values](https://bun.com/reference/globals/ReadableStream/values)(

    options?: ReadableStreamIteratorOptions

    ): ReadableStreamAsyncIterator<R>;
* ### class [ReadableStreamBYOBReader](https://bun.com/reference/globals/ReadableStreamBYOBReader)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader)

  + readonly [closed](https://bun.com/reference/globals/ReadableStreamBYOBReader/closed): Promise<void>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/closed)
  + [cancel](https://bun.com/reference/globals/ReadableStreamBYOBReader/cancel)(

    reason?: any

    ): Promise<void>;
  + [read](https://bun.com/reference/globals/ReadableStreamBYOBReader/read)<T extends ArrayBufferView<ArrayBufferLike>>(

    view: T

    ): Promise<ReadableStreamReadResult<T>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/read)
  + [releaseLock](https://bun.com/reference/globals/ReadableStreamBYOBReader/releaseLock)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/releaseLock)
* ### class [ReadableStreamBYOBRequest](https://bun.com/reference/globals/ReadableStreamBYOBRequest)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest)

  + readonly [view](https://bun.com/reference/globals/ReadableStreamBYOBRequest/view): null | ArrayBufferView<ArrayBufferLike>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/view)
  + [respond](https://bun.com/reference/globals/ReadableStreamBYOBRequest/respond)(

    bytesWritten: number

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/respond)
  + [respondWithNewView](https://bun.com/reference/globals/ReadableStreamBYOBRequest/respondWithNewView)(

    view: ArrayBufferView

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/respondWithNewView)
* ### class [ReadableStreamDefaultController](https://bun.com/reference/globals/ReadableStreamDefaultController)<R = any>

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultController)

  + readonly [desiredSize](https://bun.com/reference/globals/ReadableStreamDefaultController/desiredSize): null | number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultController/desiredSize)
  + [close](https://bun.com/reference/globals/ReadableStreamDefaultController/close)(): void;
  + [enqueue](https://bun.com/reference/globals/ReadableStreamDefaultController/enqueue)(

    chunk?: R

    ): void;
  + [error](https://bun.com/reference/globals/ReadableStreamDefaultController/error)(

    e?: any

    ): void;
* ### class [ReadableStreamDefaultReader](https://bun.com/reference/globals/ReadableStreamDefaultReader)<R = any>

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultReader)

  + readonly [closed](https://bun.com/reference/globals/ReadableStreamDefaultReader/closed): Promise<void>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/closed)
  + [cancel](https://bun.com/reference/globals/ReadableStreamDefaultReader/cancel)(

    reason?: any

    ): Promise<void>;
  + [read](https://bun.com/reference/globals/ReadableStreamDefaultReader/read)(): Promise<ReadableStreamReadResult<R>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamDefaultReader/read)

    [read](https://bun.com/reference/globals/ReadableStreamDefaultReader/read)(): Promise<[ReadableStreamDefaultReadResult](https://bun.com/reference/bun/ReadableStreamDefaultReadResult)<R>>;
  + [readMany](https://bun.com/reference/globals/ReadableStreamDefaultReader/readMany)(): [ReadableStreamDefaultReadManyResult](https://bun.com/reference/bun/ReadableStreamDefaultReadManyResult)<R> | Promise<[ReadableStreamDefaultReadManyResult](https://bun.com/reference/bun/ReadableStreamDefaultReadManyResult)<R>>;

    Only available in Bun. If there are multiple chunks in the queue, this will return all of them at the same time. Will only return a promise if the data is not immediately available.
  + [releaseLock](https://bun.com/reference/globals/ReadableStreamDefaultReader/releaseLock)(): void;
* ### class [Request](https://bun.com/reference/globals/Request)

  This Fetch API interface represents a resource request.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request)

  + readonly [body](https://bun.com/reference/globals/Request/body): null | [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/body)
  + readonly [bodyUsed](https://bun.com/reference/globals/Request/bodyUsed): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/bodyUsed)
  + readonly [cache](https://bun.com/reference/globals/Request/cache): RequestCache

    Returns the cache mode associated with request, which is a string indicating how the request will interact with the browser's cache when fetching.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/cache)
  + readonly [credentials](https://bun.com/reference/globals/Request/credentials): RequestCredentials

    Returns the credentials mode associated with request, which is a string indicating whether credentials will be sent with the request always, never, or only when sent to a same-origin URL.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/credentials)
  + readonly [destination](https://bun.com/reference/globals/Request/destination): RequestDestination

    Returns the kind of resource requested by request, e.g., "document" or "script".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/destination)
  + readonly [headers](https://bun.com/reference/globals/Request/headers): [Headers](https://bun.com/reference/globals/Headers)

    Returns a Headers object consisting of the headers associated with request. Note that headers added in the network layer by the user agent will not be accounted for in this object, e.g., the "Host" header.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/headers)
  + readonly [integrity](https://bun.com/reference/globals/Request/integrity): string

    Returns request's subresource integrity metadata, which is a cryptographic hash of the resource being fetched. Its value consists of multiple hashes separated by whitespace. [SRI]

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/integrity)
  + readonly [keepalive](https://bun.com/reference/globals/Request/keepalive): boolean

    Returns a boolean indicating whether or not request can outlive the global in which it was created.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/keepalive)
  + readonly [method](https://bun.com/reference/globals/Request/method): string

    Returns request's HTTP method, which is "GET" by default.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/method)
  + readonly [mode](https://bun.com/reference/globals/Request/mode): RequestMode

    Returns the mode associated with request, which is a string indicating whether the request will use CORS, or will be restricted to same-origin URLs.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/mode)
  + readonly [redirect](https://bun.com/reference/globals/Request/redirect): RequestRedirect

    Returns the redirect mode associated with request, which is a string indicating how redirects for the request will be handled during fetching. A request will follow redirects by default.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/redirect)
  + readonly [referrer](https://bun.com/reference/globals/Request/referrer): string

    Returns the referrer of request. Its value can be a same-origin URL if explicitly set in init, the empty string to indicate no referrer, and "about:client" when defaulting to the global's default. This is used during fetching to determine the value of the `Referer` header of the request being made.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/referrer)
  + readonly [referrerPolicy](https://bun.com/reference/globals/Request/referrerPolicy): ReferrerPolicy

    Returns the referrer policy associated with request. This is used during fetching to compute the value of the request's referrer.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/referrerPolicy)
  + readonly [signal](https://bun.com/reference/globals/Request/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Returns the signal associated with request, which is an AbortSignal object indicating whether or not request has been aborted, and its abort event handler.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/signal)
  + readonly [url](https://bun.com/reference/globals/Request/url): string

    Returns the URL of request as a string.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/url)
  + [arrayBuffer](https://bun.com/reference/globals/Request/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/arrayBuffer)
  + [blob](https://bun.com/reference/globals/Request/blob)(): Promise<[Blob](https://bun.com/reference/globals/Blob)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/blob)
  + [bytes](https://bun.com/reference/globals/Request/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/bytes)
  + [clone](https://bun.com/reference/globals/Request/clone)(): [Request](https://bun.com/reference/globals/Request);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/clone)
  + [formData](https://bun.com/reference/globals/Request/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/formData)
  + [json](https://bun.com/reference/globals/Request/json)(): Promise<any>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/json)
  + [text](https://bun.com/reference/globals/Request/text)(): Promise<string>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/text)
* ### class [Response](https://bun.com/reference/globals/Response)

  This Fetch API interface represents the response to a request.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response)

  + readonly [body](https://bun.com/reference/globals/Response/body): null | [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/body)
  + readonly [bodyUsed](https://bun.com/reference/globals/Response/bodyUsed): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/bodyUsed)
  + readonly [headers](https://bun.com/reference/globals/Response/headers): [Headers](https://bun.com/reference/globals/Headers)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/headers)
  + readonly [ok](https://bun.com/reference/globals/Response/ok): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/ok)
  + readonly [redirected](https://bun.com/reference/globals/Response/redirected): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/redirected)
  + readonly [status](https://bun.com/reference/globals/Response/status): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/status)
  + readonly [statusText](https://bun.com/reference/globals/Response/statusText): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/statusText)
  + readonly [type](https://bun.com/reference/globals/Response/type): ResponseType

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/type)
  + readonly [url](https://bun.com/reference/globals/Response/url): string

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/url)
  + [arrayBuffer](https://bun.com/reference/globals/Response/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/arrayBuffer)
  + [blob](https://bun.com/reference/globals/Response/blob)(): Promise<[Blob](https://bun.com/reference/globals/Blob)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/blob)
  + [bytes](https://bun.com/reference/globals/Response/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/bytes)
  + [clone](https://bun.com/reference/globals/Response/clone)(): [Response](https://bun.com/reference/globals/Response);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/clone)
  + [formData](https://bun.com/reference/globals/Response/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/formData)
  + [json](https://bun.com/reference/globals/Response/json)(): Promise<any>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/json)
  + [text](https://bun.com/reference/globals/Response/text)(): Promise<string>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Request/text)
  + static [error](https://bun.com/reference/globals/Response/error)(): [Response](https://bun.com/reference/globals/Response);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/error_static)
  + static [json](https://bun.com/reference/globals/Response/json)(

    data: any,

    init?: [ResponseInit](https://bun.com/reference/globals/ResponseInit)

    ): [Response](https://bun.com/reference/globals/Response);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/json_static)
  + static [redirect](https://bun.com/reference/globals/Response/redirect)(

    url: string | [URL](https://bun.com/reference/globals/URL),

    status?: number

    ): [Response](https://bun.com/reference/globals/Response);

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Response/redirect_static)
* ### class [ShadowRealm](https://bun.com/reference/globals/ShadowRealm)

  ShadowRealms are a distinct global environment, with its own global object containing its own intrinsics and built-ins (standard objects that are not bound to global variables, like the initial value of Object.prototype).

  ```
  const red = new ShadowRealm();

  // realms can import modules that will execute within it's own environment.
  // When the module is resolved, it captured the binding value, or creates a new
  // wrapped function that is connected to the callable binding.
  const redAdd = await red.importValue('./inside-code.js', 'add');

  // redAdd is a wrapped function exotic object that chains it's call to the
  // respective imported binding.
  let result = redAdd(2, 3);

  console.assert(result === 5); // yields true

  // The evaluate method can provide quick code evaluation within the constructed
  // shadowRealm without requiring any module loading, while it still requires CSP
  // relaxing.
  globalThis.someValue = 1;
  red.evaluate('globalThis.someValue = 2'); // Affects only the ShadowRealm's global
  console.assert(globalThis.someValue === 1);

  // The wrapped functions can also wrap other functions the other way around.
  const setUniqueValue =
  await red.importValue('./inside-code.js', 'setUniqueValue');

  // setUniqueValue = (cb) => (cb(globalThis.someValue) * 2);

  result = setUniqueValue((x) => x ** 3);

  console.assert(result === 16); // yields true
  ```

  + [evaluate](https://bun.com/reference/globals/ShadowRealm/evaluate)(

    sourceText: string

    ): any;
  + [importValue](https://bun.com/reference/globals/ShadowRealm/importValue)(

    specifier: string,

    bindingName: string

    ): Promise<any>;

    Creates a new [ShadowRealm](https://github.com/tc39/proposal-shadowrealm/blob/main/explainer.md#introduction)

    ```
    const red = new ShadowRealm();

    // realms can import modules that will execute within it's own environment.
    // When the module is resolved, it captured the binding value, or creates a new
    // wrapped function that is connected to the callable binding.
    const redAdd = await red.importValue('./inside-code.js', 'add');

    // redAdd is a wrapped function exotic object that chains it's call to the
    // respective imported binding.
    let result = redAdd(2, 3);

    console.assert(result === 5); // yields true

    // The evaluate method can provide quick code evaluation within the constructed
    // shadowRealm without requiring any module loading, while it still requires CSP
    // relaxing.
    globalThis.someValue = 1;
    red.evaluate('globalThis.someValue = 2'); // Affects only the ShadowRealm's global
    console.assert(globalThis.someValue === 1);

    // The wrapped functions can also wrap other functions the other way around.
    const setUniqueValue =
    await red.importValue('./inside-code.js', 'setUniqueValue');

    // setUniqueValue = (cb) => (cb(globalThis.someValue) * 2);

    result = setUniqueValue((x) => x ** 3);

    console.assert(result === 16); // yields true
    ```
* ### class [SubtleCrypto](https://bun.com/reference/globals/SubtleCrypto)

  This Web Crypto API interface provides a number of low-level cryptographic functions. It is accessed via the Crypto.subtle properties available in a window context (via Window.crypto). Available only in secure contexts.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto)

  + [decapsulateBits](https://bun.com/reference/globals/SubtleCrypto/decapsulateBits)(

    decapsulationAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier),

    decapsulationKey: [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey),

    ciphertext: [BufferSource](https://bun.com/reference/node/crypto/webcrypto/BufferSource)

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    A message recipient uses their asymmetric private key to decrypt an "encapsulated key" (ciphertext), thereby recovering a temporary symmetric key (represented as `ArrayBuffer`) which is then used to decrypt a message.

    The algorithms currently supported include:

    - `'ML-KEM-512'`
    - `'ML-KEM-768'`
    - `'ML-KEM-1024'`

    @returns

    Fulfills with `ArrayBuffer` upon success.
  + [decapsulateKey](https://bun.com/reference/globals/SubtleCrypto/decapsulateKey)(

    decapsulationAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier),

    decapsulationKey: [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey),

    ciphertext: [BufferSource](https://bun.com/reference/node/crypto/webcrypto/BufferSource),

    sharedKeyAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier) | [HmacImportParams](https://bun.com/reference/node/crypto/webcrypto/HmacImportParams) | [AesDerivedKeyParams](https://bun.com/reference/node/crypto/webcrypto/AesDerivedKeyParams) | [KmacImportParams](https://bun.com/reference/node/crypto/webcrypto/KmacImportParams),

    extractable: boolean,

    usages: [KeyUsage](https://bun.com/reference/node/crypto/webcrypto/KeyUsage)[]

    ): Promise<[CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey)>;

    A message recipient uses their asymmetric private key to decrypt an "encapsulated key" (ciphertext), thereby recovering a temporary symmetric key (represented as `CryptoKey`) which is then used to decrypt a message.

    The algorithms currently supported include:

    - `'ML-KEM-512'`
    - `'ML-KEM-768'`
    - `'ML-KEM-1024'`

    @param usages

    See [Key usages](https://nodejs.org/docs/latest-v24.x/api/webcrypto.html#cryptokeyusages).

    @returns

    Fulfills with `CryptoKey` upon success.
  + [decrypt](https://bun.com/reference/globals/SubtleCrypto/decrypt)(

    algorithm: AlgorithmIdentifier | RsaOaepParams | AesCtrParams | AesCbcParams | AesGcmParams,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    data: BufferSource

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/decrypt)
  + [deriveBits](https://bun.com/reference/globals/SubtleCrypto/deriveBits)(

    algorithm: AlgorithmIdentifier | EcdhKeyDeriveParams | HkdfParams | Pbkdf2Params,

    baseKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    length?: null | number

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/deriveBits)
  + [deriveKey](https://bun.com/reference/globals/SubtleCrypto/deriveKey)(

    algorithm: AlgorithmIdentifier | EcdhKeyDeriveParams | HkdfParams | Pbkdf2Params,

    baseKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    derivedKeyType: AlgorithmIdentifier | HkdfParams | Pbkdf2Params | AesDerivedKeyParams | HmacImportParams,

    extractable: boolean,

    keyUsages: KeyUsage[]

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/deriveKey)

    [deriveKey](https://bun.com/reference/globals/SubtleCrypto/deriveKey)(

    algorithm: AlgorithmIdentifier | EcdhKeyDeriveParams | HkdfParams | Pbkdf2Params,

    baseKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    derivedKeyType: AlgorithmIdentifier | HkdfParams | Pbkdf2Params | AesDerivedKeyParams | HmacImportParams,

    extractable: boolean,

    keyUsages: Iterable<KeyUsage>

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/deriveKey)
  + [digest](https://bun.com/reference/globals/SubtleCrypto/digest)(

    algorithm: AlgorithmIdentifier,

    data: BufferSource

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/digest)
  + [encapsulateBits](https://bun.com/reference/globals/SubtleCrypto/encapsulateBits)(

    encapsulationAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier),

    encapsulationKey: [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey)

    ): Promise<[EncapsulatedBits](https://bun.com/reference/node/crypto/webcrypto/EncapsulatedBits)>;

    Uses a message recipient's asymmetric public key to encrypt a temporary symmetric key. This encrypted key is the "encapsulated key" represented as `EncapsulatedBits`.

    The algorithms currently supported include:

    - `'ML-KEM-512'`
    - `'ML-KEM-768'`
    - `'ML-KEM-1024'`

    @returns

    Fulfills with `EncapsulatedBits` upon success.
  + [encapsulateKey](https://bun.com/reference/globals/SubtleCrypto/encapsulateKey)(

    encapsulationAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier),

    encapsulationKey: [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey),

    sharedKeyAlgorithm: [AlgorithmIdentifier](https://bun.com/reference/node/crypto/webcrypto/AlgorithmIdentifier) | [HmacImportParams](https://bun.com/reference/node/crypto/webcrypto/HmacImportParams) | [AesDerivedKeyParams](https://bun.com/reference/node/crypto/webcrypto/AesDerivedKeyParams) | [KmacImportParams](https://bun.com/reference/node/crypto/webcrypto/KmacImportParams),

    extractable: boolean,

    usages: [KeyUsage](https://bun.com/reference/node/crypto/webcrypto/KeyUsage)[]

    ): Promise<[EncapsulatedKey](https://bun.com/reference/node/crypto/webcrypto/EncapsulatedKey)>;

    Uses a message recipient's asymmetric public key to encrypt a temporary symmetric key. This encrypted key is the "encapsulated key" represented as `EncapsulatedKey`.

    The algorithms currently supported include:

    - `'ML-KEM-512'`
    - `'ML-KEM-768'`
    - `'ML-KEM-1024'`

    @param usages

    See [Key usages](https://nodejs.org/docs/latest-v24.x/api/webcrypto.html#cryptokeyusages).

    @returns

    Fulfills with `EncapsulatedKey` upon success.
  + [encrypt](https://bun.com/reference/globals/SubtleCrypto/encrypt)(

    algorithm: AlgorithmIdentifier | RsaOaepParams | AesCtrParams | AesCbcParams | AesGcmParams,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    data: BufferSource

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/encrypt)
  + [exportKey](https://bun.com/reference/globals/SubtleCrypto/exportKey)(

    format: 'jwk',

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey)

    ): Promise<JsonWebKey>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/exportKey)

    [exportKey](https://bun.com/reference/globals/SubtleCrypto/exportKey)(

    format: 'spki' | 'pkcs8' | 'raw',

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey)

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [exportKey](https://bun.com/reference/globals/SubtleCrypto/exportKey)(

    format: KeyFormat,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey)

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | JsonWebKey>;
  + [generateKey](https://bun.com/reference/globals/SubtleCrypto/generateKey)(

    algorithm: 'Ed25519' | { name: 'Ed25519' },

    extractable: boolean,

    keyUsages: readonly 'sign' | 'verify'[]

    ): Promise<[CryptoKeyPair](https://bun.com/reference/globals/CryptoKeyPair)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/generateKey)

    [generateKey](https://bun.com/reference/globals/SubtleCrypto/generateKey)(

    algorithm: RsaHashedKeyGenParams | EcKeyGenParams,

    extractable: boolean,

    keyUsages: readonly KeyUsage[]

    ): Promise<[CryptoKeyPair](https://bun.com/reference/globals/CryptoKeyPair)>;

    [generateKey](https://bun.com/reference/globals/SubtleCrypto/generateKey)(

    algorithm: Pbkdf2Params | AesKeyGenParams | HmacKeyGenParams,

    extractable: boolean,

    keyUsages: readonly KeyUsage[]

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [generateKey](https://bun.com/reference/globals/SubtleCrypto/generateKey)(

    algorithm: AlgorithmIdentifier,

    extractable: boolean,

    keyUsages: KeyUsage[]

    ): Promise<[CryptoKeyPair](https://bun.com/reference/globals/CryptoKeyPair) | [CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [generateKey](https://bun.com/reference/globals/SubtleCrypto/generateKey)(

    algorithm: AlgorithmIdentifier,

    extractable: boolean,

    keyUsages: Iterable<KeyUsage>

    ): Promise<[CryptoKeyPair](https://bun.com/reference/globals/CryptoKeyPair) | [CryptoKey](https://bun.com/reference/globals/CryptoKey)>;
  + [getPublicKey](https://bun.com/reference/globals/SubtleCrypto/getPublicKey)(

    key: [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey),

    keyUsages: [KeyUsage](https://bun.com/reference/node/crypto/webcrypto/KeyUsage)[]

    ): Promise<[CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey)>;

    Derives the public key from a given private key.

    @param key

    A private key from which to derive the corresponding public key.

    @param keyUsages

    See [Key usages](https://nodejs.org/docs/latest-v24.x/api/webcrypto.html#cryptokeyusages).

    @returns

    Fulfills with a `CryptoKey` upon success.
  + [importKey](https://bun.com/reference/globals/SubtleCrypto/importKey)(

    format: 'jwk',

    keyData: JsonWebKey,

    algorithm: AlgorithmIdentifier | HmacImportParams | RsaHashedImportParams | EcKeyImportParams | AesKeyAlgorithm,

    extractable: boolean,

    keyUsages: readonly KeyUsage[]

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/importKey)

    [importKey](https://bun.com/reference/globals/SubtleCrypto/importKey)(

    format: 'spki' | 'pkcs8' | 'raw',

    keyData: BufferSource,

    algorithm: AlgorithmIdentifier | HmacImportParams | RsaHashedImportParams | EcKeyImportParams | AesKeyAlgorithm,

    extractable: boolean,

    keyUsages: KeyUsage[]

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [importKey](https://bun.com/reference/globals/SubtleCrypto/importKey)(

    format: 'spki' | 'pkcs8' | 'raw',

    keyData: BufferSource,

    algorithm: AlgorithmIdentifier | HmacImportParams | RsaHashedImportParams | EcKeyImportParams | AesKeyAlgorithm,

    extractable: boolean,

    keyUsages: Iterable<KeyUsage>

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;
  + [sign](https://bun.com/reference/globals/SubtleCrypto/sign)(

    algorithm: AlgorithmIdentifier | RsaPssParams | EcdsaParams,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    data: BufferSource

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/sign)
  + [unwrapKey](https://bun.com/reference/globals/SubtleCrypto/unwrapKey)(

    format: KeyFormat,

    wrappedKey: BufferSource,

    unwrappingKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    unwrapAlgorithm: AlgorithmIdentifier | RsaOaepParams | AesCtrParams | AesCbcParams | AesGcmParams,

    unwrappedKeyAlgorithm: AlgorithmIdentifier | HmacImportParams | RsaHashedImportParams | EcKeyImportParams | AesKeyAlgorithm,

    extractable: boolean,

    keyUsages: KeyUsage[]

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/unwrapKey)

    [unwrapKey](https://bun.com/reference/globals/SubtleCrypto/unwrapKey)(

    format: KeyFormat,

    wrappedKey: BufferSource,

    unwrappingKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    unwrapAlgorithm: AlgorithmIdentifier | RsaOaepParams | AesCtrParams | AesCbcParams | AesGcmParams,

    unwrappedKeyAlgorithm: AlgorithmIdentifier | HmacImportParams | RsaHashedImportParams | EcKeyImportParams | AesKeyAlgorithm,

    extractable: boolean,

    keyUsages: Iterable<KeyUsage>

    ): Promise<[CryptoKey](https://bun.com/reference/globals/CryptoKey)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/unwrapKey)
  + [verify](https://bun.com/reference/globals/SubtleCrypto/verify)(

    algorithm: AlgorithmIdentifier | RsaPssParams | EcdsaParams,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    signature: BufferSource,

    data: BufferSource

    ): Promise<boolean>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/verify)
  + [wrapKey](https://bun.com/reference/globals/SubtleCrypto/wrapKey)(

    format: KeyFormat,

    key: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    wrappingKey: [CryptoKey](https://bun.com/reference/globals/CryptoKey),

    wrapAlgorithm: AlgorithmIdentifier | RsaOaepParams | AesCtrParams | AesCbcParams | AesGcmParams

    ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/SubtleCrypto/wrapKey)
* ### class [TextDecoder](https://bun.com/reference/globals/TextDecoder)

  A decoder for a specific method, that is a specific character encoding, like utf-8, iso-8859-2, koi8, cp1261, gbk, etc. A decoder takes a stream of bytes as input and emits a stream of code points. For a more scalable, non-native library, see StringView – a C-like representation of strings based on typed arrays.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder)

  + readonly [encoding](https://bun.com/reference/globals/TextDecoder/encoding): string

    Returns encoding's name, lowercased.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/encoding)
  + readonly [fatal](https://bun.com/reference/globals/TextDecoder/fatal): boolean

    Returns true if error mode is "fatal", otherwise false.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/fatal)
  + readonly [ignoreBOM](https://bun.com/reference/globals/TextDecoder/ignoreBOM): boolean

    Returns the value of ignore BOM.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/ignoreBOM)
  + [decode](https://bun.com/reference/globals/TextDecoder/decode)(

    input?: AllowSharedBufferSource,

    options?: TextDecodeOptions

    ): string;

    Returns the result of running encoding's decoder. The method can be invoked zero or more times with options's stream set to true, and then once without options's stream (or set to false), to process a fragmented input. If the invocation without options's stream (or set to false) has no input, it's clearest to omit both arguments.

    ```
    var string = "", decoder = new TextDecoder(encoding), buffer;
    while(buffer = next_chunk()) {
      string += decoder.decode(buffer, {stream:true});
    }
    string += decoder.decode(); // end-of-queue
    ```

    If the error mode is "fatal" and encoding's decoder returns error, throws a TypeError.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/decode)
* ### class [TextDecoderStream](https://bun.com/reference/globals/TextDecoderStream)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoderStream)

  + readonly [encoding](https://bun.com/reference/globals/TextDecoderStream/encoding): string

    Returns encoding's name, lowercased.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/encoding)
  + readonly [fatal](https://bun.com/reference/globals/TextDecoderStream/fatal): boolean

    Returns true if error mode is "fatal", otherwise false.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/fatal)
  + readonly [ignoreBOM](https://bun.com/reference/globals/TextDecoderStream/ignoreBOM): boolean

    Returns the value of ignore BOM.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextDecoder/ignoreBOM)
  + readonly [readable](https://bun.com/reference/globals/TextDecoderStream/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<string>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/readable)
  + readonly [writable](https://bun.com/reference/globals/TextDecoderStream/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<BufferSource>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/writable)
* ### class [TextEncoder](https://bun.com/reference/globals/TextEncoder)

  TextEncoder takes a stream of code points as input and emits a stream of bytes. For a more scalable, non-native library, see StringView – a C-like representation of strings based on typed arrays.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoder)

  + readonly [encoding](https://bun.com/reference/globals/TextEncoder/encoding): string

    Returns "utf-8".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoder/encoding)
  + [encode](https://bun.com/reference/globals/TextEncoder/encode)(

    input?: string

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array);

    Returns the result of running UTF-8's encoder.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoder/encode)
  + [encodeInto](https://bun.com/reference/globals/TextEncoder/encodeInto)(

    source: string,

    destination: [Uint8Array](https://bun.com/reference/globals/Uint8Array)

    ): TextEncoderEncodeIntoResult;

    Runs the UTF-8 encoder on source, stores the result of that operation into destination, and returns the progress made as an object wherein read is the number of converted code units of source and written is the number of bytes modified in destination.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoder/encodeInto)

    [encodeInto](https://bun.com/reference/globals/TextEncoder/encodeInto)(

    src?: string,

    dest?: [BufferSource](https://bun.com/reference/bun/BufferSource)

    ): [EncodeIntoResult](https://bun.com/reference/node/util/EncodeIntoResult);

    UTF-8 encodes the `src` string to the `dest` Uint8Array and returns an object containing the read Unicode code units and written UTF-8 bytes.

    ```
    const encoder = new TextEncoder();
    const src = 'this is some data';
    const dest = new Uint8Array(10);
    const { read, written } = encoder.encodeInto(src, dest);
    ```

    @param src

    The text to encode.

    @param dest

    The array to hold the encode result.
* ### class [TextEncoderStream](https://bun.com/reference/globals/TextEncoderStream)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoderStream)

  + readonly [encoding](https://bun.com/reference/globals/TextEncoderStream/encoding): string

    Returns "utf-8".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TextEncoder/encoding)
  + readonly [readable](https://bun.com/reference/globals/TextEncoderStream/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/readable)
  + readonly [writable](https://bun.com/reference/globals/TextEncoderStream/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<string>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/CompressionStream/writable)
* ### class [TransformStream](https://bun.com/reference/globals/TransformStream)<I = any, O = any>

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TransformStream)

  + readonly [readable](https://bun.com/reference/globals/TransformStream/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<O>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TransformStream/readable)
  + readonly [writable](https://bun.com/reference/globals/TransformStream/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<I>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TransformStream/writable)
* ### class [TransformStreamDefaultController](https://bun.com/reference/globals/TransformStreamDefaultController)<O = any>

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/TransformStreamDefaultController)

  + readonly [desiredSize](https://bun.com/reference/globals/TransformStreamDefaultController/desiredSize): null | number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/TransformStreamDefaultController/desiredSize)
  + [enqueue](https://bun.com/reference/globals/TransformStreamDefaultController/enqueue)(

    chunk?: O

    ): void;
  + [error](https://bun.com/reference/globals/TransformStreamDefaultController/error)(

    reason?: any

    ): void;
  + [terminate](https://bun.com/reference/globals/TransformStreamDefaultController/terminate)(): void;
* ### class [Uint8Array](https://bun.com/reference/globals/Uint8Array)<TArrayBuffer extends ArrayBufferLike = ArrayBufferLike>

  A typed array of 8-bit unsigned integer values. The contents are initialized to 0. If the requested number of bytes could not be allocated an exception is raised.

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/globals/Uint8Array/[toStringTag]): 'Uint8Array'
  + readonly [buffer](https://bun.com/reference/globals/Uint8Array/buffer): TArrayBuffer

    The ArrayBuffer instance referenced by the array.
  + readonly [byteLength](https://bun.com/reference/globals/Uint8Array/byteLength): number

    The length in bytes of the array.
  + readonly [byteOffset](https://bun.com/reference/globals/Uint8Array/byteOffset): number

    The offset in bytes of the array.
  + readonly [BYTES\_PER\_ELEMENT](https://bun.com/reference/globals/Uint8Array/BYTES_PER_ELEMENT): number

    The size in bytes of each element in the array.
  + readonly [length](https://bun.com/reference/globals/Uint8Array/length): number

    The length of the array.
  + [[Symbol.iterator]](https://bun.com/reference/globals/Uint8Array/[iterator])(): ArrayIterator<number>;
  + [at](https://bun.com/reference/globals/Uint8Array/at)(

    index: number

    ): undefined | number;

    Returns the item located at the specified index.

    @param index

    The zero-based index of the desired code unit. A negative index will count back from the last item.
  + [copyWithin](https://bun.com/reference/globals/Uint8Array/copyWithin)(

    target: number,

    start: number,

    end?: number

    ): this;

    Returns the this object after copying a section of the array identified by start and end to the same array starting at position target

    @param target

    If target is negative, it is treated as length+target where length is the length of the array.

    @param start

    If start is negative, it is treated as length+start. If end is negative, it is treated as length+end.

    @param end

    If not specified, length of the this object is used as its default value.
  + [entries](https://bun.com/reference/globals/Uint8Array/entries)(): ArrayIterator<[number, number]>;

    Returns an array of key, value pairs for every entry in the array
  + [every](https://bun.com/reference/globals/Uint8Array/every)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): boolean;

    Determines whether all the members of an array satisfy the specified test.

    @param predicate

    A function that accepts up to three arguments. The every method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value false, or until the end of the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [fill](https://bun.com/reference/globals/Uint8Array/fill)(

    value: number,

    start?: number,

    end?: number

    ): this;

    Changes all array elements from `start` to `end` index to a static `value` and returns the modified array

    @param value

    value to fill array section with

    @param start

    index to start filling the array at. If start is negative, it is treated as length+start where length is the length of the array.

    @param end

    index to stop filling the array at. If end is negative, it is treated as length+end.
  + [filter](https://bun.com/reference/globals/Uint8Array/filter)(

    predicate: (value: number, index: number, array: this) => any,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns the elements of an array that meet the condition specified in a callback function.

    @param predicate

    A function that accepts up to three arguments. The filter method calls the predicate function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [find](https://bun.com/reference/globals/Uint8Array/find)(

    predicate: (value: number, index: number, obj: this) => boolean,

    thisArg?: any

    ): undefined | number;

    Returns the value of the first element in the array where predicate is true, and undefined otherwise.

    @param predicate

    find calls predicate once for each element of the array, in ascending order, until it finds one where predicate returns true. If such an element is found, find immediately returns that element value. Otherwise, find returns undefined.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [findIndex](https://bun.com/reference/globals/Uint8Array/findIndex)(

    predicate: (value: number, index: number, obj: this) => boolean,

    thisArg?: any

    ): number;

    Returns the index of the first element in the array where predicate is true, and -1 otherwise.

    @param predicate

    find calls predicate once for each element of the array, in ascending order, until it finds one where predicate returns true. If such an element is found, findIndex immediately returns that element index. Otherwise, findIndex returns -1.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [findLast](https://bun.com/reference/globals/Uint8Array/findLast)<S extends number>(

    predicate: (value: number, index: number, array: this) => value is S,

    thisArg?: any

    ): undefined | S;

    Returns the value of the last element in the array where predicate is true, and undefined otherwise.

    @param predicate

    findLast calls predicate once for each element of the array, in descending order, until it finds one where predicate returns true. If such an element is found, findLast immediately returns that element value. Otherwise, findLast returns undefined.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.

    [findLast](https://bun.com/reference/globals/Uint8Array/findLast)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): undefined | number;
  + [findLastIndex](https://bun.com/reference/globals/Uint8Array/findLastIndex)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): number;

    Returns the index of the last element in the array where predicate is true, and -1 otherwise.

    @param predicate

    findLastIndex calls predicate once for each element of the array, in descending order, until it finds one where predicate returns true. If such an element is found, findLastIndex immediately returns that element index. Otherwise, findLastIndex returns -1.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [forEach](https://bun.com/reference/globals/Uint8Array/forEach)(

    callbackfn: (value: number, index: number, array: this) => void,

    thisArg?: any

    ): void;

    Performs the specified action for each element in an array.

    @param callbackfn

    A function that accepts up to three arguments. forEach calls the callbackfn function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
  + [includes](https://bun.com/reference/globals/Uint8Array/includes)(

    searchElement: number,

    fromIndex?: number

    ): boolean;

    Determines whether an array includes a certain element, returning true or false as appropriate.

    @param searchElement

    The element to search for.

    @param fromIndex

    The position in this array at which to begin searching for searchElement.
  + [indexOf](https://bun.com/reference/globals/Uint8Array/indexOf)(

    searchElement: number,

    fromIndex?: number

    ): number;

    Returns the index of the first occurrence of a value in an array.

    @param searchElement

    The value to locate in the array.

    @param fromIndex

    The array index at which to begin the search. If fromIndex is omitted, the search starts at index 0.
  + [join](https://bun.com/reference/globals/Uint8Array/join)(

    separator?: string

    ): string;

    Adds all the elements of an array separated by the specified separator string.

    @param separator

    A string used to separate one element of an array from the next in the resulting String. If omitted, the array elements are separated with a comma.
  + [keys](https://bun.com/reference/globals/Uint8Array/keys)(): ArrayIterator<number>;

    Returns an list of keys in the array
  + [lastIndexOf](https://bun.com/reference/globals/Uint8Array/lastIndexOf)(

    searchElement: number,

    fromIndex?: number

    ): number;

    Returns the index of the last occurrence of a value in an array.

    @param searchElement

    The value to locate in the array.

    @param fromIndex

    The array index at which to begin the search. If fromIndex is omitted, the search starts at index 0.
  + [map](https://bun.com/reference/globals/Uint8Array/map)(

    callbackfn: (value: number, index: number, array: this) => number,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Calls a defined callback function on each element of an array, and returns an array that contains the results.

    @param callbackfn

    A function that accepts up to three arguments. The map method calls the callbackfn function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
  + [reduce](https://bun.com/reference/globals/Uint8Array/reduce)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number

    ): number;

    Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduce method calls the callbackfn function one time for each element in the array.

    [reduce](https://bun.com/reference/globals/Uint8Array/reduce)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number,

    initialValue: number

    ): number;

    [reduce](https://bun.com/reference/globals/Uint8Array/reduce)<U>(

    callbackfn: (previousValue: U, currentValue: number, currentIndex: number, array: this) => U,

    initialValue: U

    ): U;

    Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduce method calls the callbackfn function one time for each element in the array.

    @param initialValue

    If initialValue is specified, it is used as the initial value to start the accumulation. The first call to the callbackfn function provides this value as an argument instead of an array value.
  + [reduceRight](https://bun.com/reference/globals/Uint8Array/reduceRight)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number

    ): number;

    Calls the specified callback function for all the elements in an array, in descending order. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduceRight method calls the callbackfn function one time for each element in the array.

    [reduceRight](https://bun.com/reference/globals/Uint8Array/reduceRight)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number,

    initialValue: number

    ): number;

    [reduceRight](https://bun.com/reference/globals/Uint8Array/reduceRight)<U>(

    callbackfn: (previousValue: U, currentValue: number, currentIndex: number, array: this) => U,

    initialValue: U

    ): U;

    Calls the specified callback function for all the elements in an array, in descending order. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduceRight method calls the callbackfn function one time for each element in the array.

    @param initialValue

    If initialValue is specified, it is used as the initial value to start the accumulation. The first call to the callbackfn function provides this value as an argument instead of an array value.
  + [reverse](https://bun.com/reference/globals/Uint8Array/reverse)(): this;

    Reverses the elements in an Array.
  + [set](https://bun.com/reference/globals/Uint8Array/set)(

    array: ArrayLike<number>,

    offset?: number

    ): void;

    Sets a value or an array of values.

    @param array

    A typed or untyped array of values to set.

    @param offset

    The index in the current array at which the values are to be written.
  + [setFromBase64](https://bun.com/reference/globals/Uint8Array/setFromBase64)(

    base64: string,

    offset?: number

    ): { read: number; written: number };

    Set the contents of the Uint8Array from a base64 encoded string

    @param base64

    The base64 encoded string to decode into the array

    @param offset

    Optional starting index to begin setting the decoded bytes (default: 0)
  + [setFromHex](https://bun.com/reference/globals/Uint8Array/setFromHex)(

    hex: string

    ): { read: number; written: number };

    Set the contents of the Uint8Array from a hex encoded string

    @param hex

    The hex encoded string to decode into the array. The string must have an even number of characters, be valid hexadecimal characters and contain no whitespace.
  + [slice](https://bun.com/reference/globals/Uint8Array/slice)(

    start?: number,

    end?: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns a section of an array.

    @param start

    The beginning of the specified portion of the array.

    @param end

    The end of the specified portion of the array. This is exclusive of the element at the index 'end'.
  + [some](https://bun.com/reference/globals/Uint8Array/some)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): boolean;

    Determines whether the specified callback function returns true for any element of an array.

    @param predicate

    A function that accepts up to three arguments. The some method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value true, or until the end of the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [sort](https://bun.com/reference/globals/Uint8Array/sort)(

    compareFn?: (a: number, b: number) => number

    ): this;

    Sorts an array.

    @param compareFn

    Function used to determine the order of the elements. It is expected to return a negative value if first argument is less than second argument, zero if they're equal and a positive value otherwise. If omitted, the elements are sorted in ascending order.

    ```
    [11,2,22,1].sort((a, b) => a - b)
    ```
  + [subarray](https://bun.com/reference/globals/Uint8Array/subarray)(

    begin?: number,

    end?: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<TArrayBuffer>;

    Gets a new Uint8Array view of the ArrayBuffer store for this array, referencing the elements at begin, inclusive, up to end, exclusive.

    @param begin

    The index of the beginning of the array.

    @param end

    The index of the end of the array.
  + [toBase64](https://bun.com/reference/globals/Uint8Array/toBase64)(

    options?: { alphabet: 'base64' | 'base64url'; omitPadding: boolean }

    ): string;

    Convert the Uint8Array to a base64 encoded string

    @returns

    The base64 encoded string representation of the Uint8Array
  + [toHex](https://bun.com/reference/globals/Uint8Array/toHex)(): string;

    Convert the Uint8Array to a hex encoded string

    @returns

    The hex encoded string representation of the Uint8Array
  + [toLocaleString](https://bun.com/reference/globals/Uint8Array/toLocaleString)(): string;

    Converts a number to a string by using the current locale.

    [toLocaleString](https://bun.com/reference/globals/Uint8Array/toLocaleString)(

    locales: string | string[],

    options?: NumberFormatOptions

    ): string;
  + [toReversed](https://bun.com/reference/globals/Uint8Array/toReversed)(): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies the array and returns the copy with the elements in reverse order.
  + [toSorted](https://bun.com/reference/globals/Uint8Array/toSorted)(

    compareFn?: (a: number, b: number) => number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies and sorts the array.

    @param compareFn

    Function used to determine the order of the elements. It is expected to return a negative value if the first argument is less than the second argument, zero if they're equal, and a positive value otherwise. If omitted, the elements are sorted in ascending order.

    ```
    const myNums = Uint8Array.from([11, 2, 22, 1]);
    myNums.toSorted((a, b) => a - b) // Uint8Array(4) [1, 2, 11, 22]
    ```
  + [toString](https://bun.com/reference/globals/Uint8Array/toString)(): string;

    Returns a string representation of an array.
  + [valueOf](https://bun.com/reference/globals/Uint8Array/valueOf)(): this;

    Returns the primitive value of the specified object.
  + [values](https://bun.com/reference/globals/Uint8Array/values)(): ArrayIterator<number>;

    Returns an list of values in the array
  + [with](https://bun.com/reference/globals/Uint8Array/with)(

    index: number,

    value: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies the array and inserts the given number at the provided index.

    @param index

    The index of the value to overwrite. If the index is negative, then it replaces from the end of the array.

    @param value

    The value to insert into the copied array.

    @returns

    A copy of the original array with the inserted value.
* ### class [URLSearchParams](https://bun.com/reference/globals/URLSearchParams)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams)

  + readonly [size](https://bun.com/reference/globals/URLSearchParams/size): number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/size)
  + [[Symbol.iterator]](https://bun.com/reference/globals/URLSearchParams/[iterator])(): URLSearchParamsIterator<[string, string]>;
  + [append](https://bun.com/reference/globals/URLSearchParams/append)(

    name: string,

    value: string

    ): void;

    Appends a specified key/value pair as a new search parameter.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/append)
  + [delete](https://bun.com/reference/globals/URLSearchParams/delete)(

    name: string,

    value?: string

    ): void;

    Deletes the given search parameter, and its associated value, from the list of all search parameters.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/delete)
  + [entries](https://bun.com/reference/globals/URLSearchParams/entries)(): URLSearchParamsIterator<[string, string]>;

    Returns an array of key, value pairs for every entry in the search params.
  + [forEach](https://bun.com/reference/globals/URLSearchParams/forEach)(

    callbackfn: (value: string, key: string, parent: [URLSearchParams](https://bun.com/reference/globals/URLSearchParams)) => void,

    thisArg?: any

    ): void;

    Iterates over each name-value pair in the query and invokes the given function.

    ```
    const myURL = new URL('https://example.org/?a=b&#x26;c=d');
    myURL.searchParams.forEach((value, name, searchParams) => {
      console.log(name, value, myURL.searchParams === searchParams);
    });
    // Prints:
    //   a b true
    //   c d true
    ```

    @param callbackfn

    Invoked for each name-value pair in the query

    @param thisArg

    To be used as `this` value for when `fn` is called
  + [get](https://bun.com/reference/globals/URLSearchParams/get)(

    name: string

    ): null | string;

    Returns the first value associated to the given search parameter.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/get)
  + [getAll](https://bun.com/reference/globals/URLSearchParams/getAll)(

    name: string

    ): string[];

    Returns all the values association with a given search parameter.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/getAll)
  + [has](https://bun.com/reference/globals/URLSearchParams/has)(

    name: string,

    value?: string

    ): boolean;

    Returns a Boolean indicating if such a search parameter exists.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/has)
  + [keys](https://bun.com/reference/globals/URLSearchParams/keys)(): URLSearchParamsIterator<string>;

    Returns a list of keys in the search params.
  + [set](https://bun.com/reference/globals/URLSearchParams/set)(

    name: string,

    value: string

    ): void;

    Sets the value associated to a given search parameter to the given value. If there were several values, delete the others.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/set)
  + [sort](https://bun.com/reference/globals/URLSearchParams/sort)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/URLSearchParams/sort)
  + [toJSON](https://bun.com/reference/globals/URLSearchParams/toJSON)(): Record<string, string>;
  + [toString](https://bun.com/reference/globals/URLSearchParams/toString)(): string;

    Returns a string containing a query string suitable for use in a URL. Does not include the question mark.
  + [values](https://bun.com/reference/globals/URLSearchParams/values)(): URLSearchParamsIterator<string>;

    Returns a list of values in the search params.
* ### class [WritableStream](https://bun.com/reference/globals/WritableStream)<W = any>

  This Streams API interface provides a standard abstraction for writing streaming data to a destination, known as a sink. This object comes with built-in backpressure and queuing.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStream)

  + readonly [locked](https://bun.com/reference/globals/WritableStream/locked): boolean

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStream/locked)
  + [abort](https://bun.com/reference/globals/WritableStream/abort)(

    reason?: any

    ): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStream/abort)
  + [close](https://bun.com/reference/globals/WritableStream/close)(): Promise<void>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStream/close)
  + [getWriter](https://bun.com/reference/globals/WritableStream/getWriter)(): [WritableStreamDefaultWriter](https://bun.com/reference/globals/WritableStreamDefaultWriter)<W>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStream/getWriter)
* ### class [WritableStreamDefaultController](https://bun.com/reference/globals/WritableStreamDefaultController)

  This Streams API interface represents a controller allowing control of a WritableStream's state. When constructing a WritableStream, the underlying sink is given a corresponding WritableStreamDefaultController instance to manipulate.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultController)

  + readonly [signal](https://bun.com/reference/globals/WritableStreamDefaultController/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultController/signal)
  + [error](https://bun.com/reference/globals/WritableStreamDefaultController/error)(

    e?: any

    ): void;
* ### class [WritableStreamDefaultWriter](https://bun.com/reference/globals/WritableStreamDefaultWriter)<W = any>

  This Streams API interface is the object returned by WritableStream.getWriter() and once created locks the < writer to the WritableStream ensuring that no other streams can write to the underlying sink.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultWriter)

  + readonly [closed](https://bun.com/reference/globals/WritableStreamDefaultWriter/closed): Promise<void>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultWriter/closed)
  + readonly [desiredSize](https://bun.com/reference/globals/WritableStreamDefaultWriter/desiredSize): null | number

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultWriter/desiredSize)
  + readonly [ready](https://bun.com/reference/globals/WritableStreamDefaultWriter/ready): Promise<void>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WritableStreamDefaultWriter/ready)
  + [abort](https://bun.com/reference/globals/WritableStreamDefaultWriter/abort)(

    reason?: any

    ): Promise<void>;
  + [close](https://bun.com/reference/globals/WritableStreamDefaultWriter/close)(): Promise<void>;
  + [releaseLock](https://bun.com/reference/globals/WritableStreamDefaultWriter/releaseLock)(): void;
  + [write](https://bun.com/reference/globals/WritableStreamDefaultWriter/write)(

    chunk?: W

    ): Promise<void>;

## Type definitions

* ### namespace [console](https://bun.com/reference/globals/console)

  The `console` module provides a simple debugging console that is similar to the JavaScript console mechanism provided by web browsers.

  The module exports two specific components:

  + A `Console` class with methods such as `console.log()`, `console.error()` and `console.warn()` that can be used to write to any Node.js stream.
  + A global `console` instance configured to write to [`process.stdout`](https://nodejs.org/docs/latest-v24.x/api/process.html#processstdout) and [`process.stderr`](https://nodejs.org/docs/latest-v24.x/api/process.html#processstderr). The global `console` can be used without importing the `node:console` module.

  ***Warning***: The global console object's methods are neither consistently synchronous like the browser APIs they resemble, nor are they consistently asynchronous like all other Node.js streams. See the [`note on process I/O`](https://nodejs.org/docs/latest-v24.x/api/process.html#a-note-on-process-io) for more information.

  Example using the global `console`:

  ```
  console.log('hello world');
  // Prints: hello world, to stdout
  console.log('hello %s', 'world');
  // Prints: hello world, to stdout
  console.error(new Error('Whoops, something bad happened'));
  // Prints error message and stack trace to stderr:
  //   Error: Whoops, something bad happened
  //     at [eval]:5:15
  //     at Script.runInThisContext (node:vm:132:18)
  //     at Object.runInThisContext (node:vm:309:38)
  //     at node:internal/process/execution:77:19
  //     at [eval]-wrapper:6:22
  //     at evalScript (node:internal/process/execution:76:60)
  //     at node:internal/main/eval_string:23:3

  const name = 'Will Robinson';
  console.warn(`Danger ${name}! Danger!`);
  // Prints: Danger Will Robinson! Danger!, to stderr
  ```

  Example using the `Console` class:

  ```
  const out = getStreamSomehow();
  const err = getStreamSomehow();
  const myConsole = new console.Console(out, err);

  myConsole.log('hello world');
  // Prints: hello world, to out
  myConsole.log('hello %s', 'world');
  // Prints: hello world, to out
  myConsole.error(new Error('Whoops, something bad happened'));
  // Prints: [Error: Whoops, something bad happened], to err

  const name = 'Will Robinson';
  myConsole.warn(`Danger ${name}! Danger!`);
  // Prints: Danger Will Robinson! Danger!, to err
  ```

  + ### interface [ConsoleConstructor](https://bun.com/reference/globals/console/ConsoleConstructor)

    - constructor ConsoleConstructor(

      stdout: WritableStream,

      stderr?: WritableStream,

      ignoreErrors?: boolean

      ): [Console](https://bun.com/reference/globals/Console);

      constructor ConsoleConstructor(

      options: [ConsoleConstructorOptions](https://bun.com/reference/globals/console/ConsoleConstructorOptions)

      ): [Console](https://bun.com/reference/globals/Console);
    - [prototype](https://bun.com/reference/globals/console/ConsoleConstructor/prototype): [Console](https://bun.com/reference/globals/Console)
  + ### interface [ConsoleConstructorOptions](https://bun.com/reference/globals/console/ConsoleConstructorOptions)

    - [colorMode](https://bun.com/reference/globals/console/ConsoleConstructorOptions/colorMode)?: boolean | 'auto'

      Set color support for this `Console` instance. Setting to true enables coloring while inspecting values. Setting to `false` disables coloring while inspecting values. Setting to `'auto'` makes color support depend on the value of the `isTTY` property and the value returned by `getColorDepth()` on the respective stream. This option can not be used, if `inspectOptions.colors` is set as well.
    - [groupIndentation](https://bun.com/reference/globals/console/ConsoleConstructorOptions/groupIndentation)?: number

      Set group indentation.
    - [ignoreErrors](https://bun.com/reference/globals/console/ConsoleConstructorOptions/ignoreErrors)?: boolean

      Ignore errors when writing to the underlying streams.
    - [inspectOptions](https://bun.com/reference/globals/console/ConsoleConstructorOptions/inspectOptions)?: [InspectOptions](https://bun.com/reference/node/util/InspectOptions) | ReadonlyMap<WritableStream, [InspectOptions](https://bun.com/reference/node/util/InspectOptions)>

      Specifies options that are passed along to `util.inspect()`. Can be an options object or, if different options for stdout and stderr are desired, a `Map` from stream objects to options.
    - [stderr](https://bun.com/reference/globals/console/ConsoleConstructorOptions/stderr)?: WritableStream
    - [stdout](https://bun.com/reference/globals/console/ConsoleConstructorOptions/stdout): WritableStream
* ### interface [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

  + [capture](https://bun.com/reference/globals/AddEventListenerOptions/capture)?: boolean
  + [once](https://bun.com/reference/globals/AddEventListenerOptions/once)?: boolean
  + [passive](https://bun.com/reference/globals/AddEventListenerOptions/passive)?: boolean
  + [signal](https://bun.com/reference/globals/AddEventListenerOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
* ### interface [ArrayBufferConstructor](https://bun.com/reference/globals/ArrayBufferConstructor)

  + constructor ArrayBufferConstructor(

    byteLength: number

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    constructor (): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

    constructor ArrayBufferConstructor(

    byteLength: number,

    options: { maxByteLength: number }

    ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);
  + readonly [[Symbol.species]](https://bun.com/reference/globals/ArrayBufferConstructor/[species]): [ArrayBufferConstructor](https://bun.com/reference/globals/ArrayBufferConstructor)
  + readonly [prototype](https://bun.com/reference/globals/ArrayBufferConstructor/prototype): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)
  + [isView](https://bun.com/reference/globals/ArrayBufferConstructor/isView)(

    arg: any

    ): arg is ArrayBufferView<ArrayBufferLike>;
* ### interface [ArrayConstructor](https://bun.com/reference/globals/ArrayConstructor)

  + constructor ArrayConstructor(

    arrayLength?: number

    ): any[];

    constructor ArrayConstructor<T>(

    arrayLength: number

    ): T[];

    constructor ArrayConstructor<T>(

    ...items: T[]

    ): T[];
  + readonly [[Symbol.species]](https://bun.com/reference/globals/ArrayConstructor/[species]): [ArrayConstructor](https://bun.com/reference/globals/ArrayConstructor)
  + readonly [prototype](https://bun.com/reference/globals/ArrayConstructor/prototype): any[]
  + [from](https://bun.com/reference/globals/ArrayConstructor/from)<T>(

    arrayLike: ArrayLike<T>

    ): T[];

    Creates an array from an array-like object.

    @param arrayLike

    An array-like object to convert to an array.

    [from](https://bun.com/reference/globals/ArrayConstructor/from)<T, U>(

    arrayLike: ArrayLike<T>,

    mapfn: (v: T, k: number) => U,

    thisArg?: any

    ): U[];

    Creates an array from an iterable object.

    @param arrayLike

    An array-like object to convert to an array.

    @param mapfn

    A mapping function to call on every element of the array.

    @param thisArg

    Value of 'this' used to invoke the mapfn.

    [from](https://bun.com/reference/globals/ArrayConstructor/from)<T>(

    iterable: Iterable<T, any, any> | ArrayLike<T>

    ): T[];

    Creates an array from an iterable object.

    @param iterable

    An iterable object to convert to an array.

    [from](https://bun.com/reference/globals/ArrayConstructor/from)<T, U>(

    iterable: Iterable<T, any, any> | ArrayLike<T>,

    mapfn: (v: T, k: number) => U,

    thisArg?: any

    ): U[];

    Creates an array from an iterable object.

    @param iterable

    An iterable object to convert to an array.

    @param mapfn

    A mapping function to call on every element of the array.

    @param thisArg

    Value of 'this' used to invoke the mapfn.
  + [fromAsync](https://bun.com/reference/globals/ArrayConstructor/fromAsync)<T>(

    iterableOrArrayLike: AsyncIterable<T, any, any> | Iterable<T | PromiseLike<T>, any, any> | ArrayLike<T | PromiseLike<T>>

    ): Promise<T[]>;

    Creates an array from an async iterator or iterable object.

    @param iterableOrArrayLike

    An async iterator or array-like object to convert to an array.

    [fromAsync](https://bun.com/reference/globals/ArrayConstructor/fromAsync)<T, U>(

    iterableOrArrayLike: AsyncIterable<T, any, any> | Iterable<T, any, any> | ArrayLike<T>,

    mapFn: (value: Awaited<T>, index: number) => U,

    thisArg?: any

    ): Promise<Awaited<U>[]>;

    Creates an array from an async iterator or iterable object.

    @param iterableOrArrayLike

    An async iterator or array-like object to convert to an array.

    @param thisArg

    Value of 'this' used when executing mapfn.

    [fromAsync](https://bun.com/reference/globals/ArrayConstructor/fromAsync)<T>(

    arrayLike: AsyncIterable<T, any, any> | Iterable<T, any, any> | ArrayLike<T>

    ): Promise<Awaited<T>[]>;

    Create an array from an iterable or async iterable object. Values from the iterable are awaited.

    ```
    await Array.fromAsync([1]); // [1]
    await Array.fromAsync([Promise.resolve(1)]); // [1]
    await Array.fromAsync((async function*() { yield 1 })()); // [1]
    ```

    @param arrayLike

    The iterable or async iterable to convert to an array.

    @returns

    A Promise whose fulfillment is a new Array instance containing the values from the iterator.

    [fromAsync](https://bun.com/reference/globals/ArrayConstructor/fromAsync)<T, U>(

    arrayLike: AsyncIterable<T, any, any> | Iterable<T, any, any> | ArrayLike<T>,

    mapFn?: (value: T, index: number) => U,

    thisArg?: any

    ): Promise<Awaited<U>[]>;

    Create an array from an iterable or async iterable object. Values from the iterable are awaited. Results of the map function are also awaited.

    ```
    await Array.fromAsync([1]); // [1]
    await Array.fromAsync([Promise.resolve(1)]); // [1]
    await Array.fromAsync((async function*() { yield 1 })()); // [1]
    await Array.fromAsync([1], (n) => n + 1); // [2]
    await Array.fromAsync([1], (n) => Promise.resolve(n + 1)); // [2]
    ```

    @param arrayLike

    The iterable or async iterable to convert to an array.

    @param mapFn

    A mapper function that transforms each element of `arrayLike` after awaiting them.

    @param thisArg

    The `this` to which `mapFn` is bound.

    @returns

    A Promise whose fulfillment is a new Array instance containing the values from the iterator.
  + [isArray](https://bun.com/reference/globals/ArrayConstructor/isArray)(

    arg: any

    ): arg is any[];
  + [of](https://bun.com/reference/globals/ArrayConstructor/of)<T>(

    ...items: T[]

    ): T[];

    Returns a new array from a set of elements.

    @param items

    A set of elements to include in the new array object.
* ### interface [BlobPropertyBag](https://bun.com/reference/globals/BlobPropertyBag)

  + [endings](https://bun.com/reference/globals/BlobPropertyBag/endings)?: EndingType
  + [type](https://bun.com/reference/globals/BlobPropertyBag/type)?: string

    Set a default "type". Not yet implemented.
* ### interface [BunFetchRequestInit](https://bun.com/reference/globals/BunFetchRequestInit)

  BunFetchRequestInit represents additional options that Bun supports in `fetch()` only.

  Bun extends the `fetch` API with some additional options, except this interface is not quite a `RequestInit`, because they won't work if passed to `new Request()`. This is why it's a separate type.

  + [body](https://bun.com/reference/globals/BunFetchRequestInit/body)?: null | BodyInit

    A BodyInit object or null to set request's body.
  + [cache](https://bun.com/reference/globals/BunFetchRequestInit/cache)?: RequestCache

    A string indicating how the request will interact with the browser's cache to set request's cache.
  + [credentials](https://bun.com/reference/globals/BunFetchRequestInit/credentials)?: RequestCredentials

    A string indicating whether credentials will be sent with the request always, never, or only when sent to a same-origin URL. Sets request's credentials.
  + [decompress](https://bun.com/reference/globals/BunFetchRequestInit/decompress)?: boolean

    Control automatic decompression of the response body. When set to `false`, the response body will not be automatically decompressed, and the `Content-Encoding` header will be preserved. This can improve performance when you need to handle compressed data manually or forward it as-is. This is a custom property that is not part of the Fetch API specification.

    ```
    // Disable automatic decompression for a proxy server
    const response = await fetch("https://example.com/api", {
      decompress: false
    });
    // response.headers.get('content-encoding') might be 'gzip' or 'br'
    ```
  + [headers](https://bun.com/reference/globals/BunFetchRequestInit/headers)?: HeadersInit

    A Headers object, an object literal, or an array of two-item arrays to set request's headers.
  + [integrity](https://bun.com/reference/globals/BunFetchRequestInit/integrity)?: string

    A cryptographic hash of the resource to be fetched by request. Sets request's integrity.
  + [keepalive](https://bun.com/reference/globals/BunFetchRequestInit/keepalive)?: boolean

    A boolean to set request's keepalive.
  + [method](https://bun.com/reference/globals/BunFetchRequestInit/method)?: string

    A string to set request's method.
  + [mode](https://bun.com/reference/globals/BunFetchRequestInit/mode)?: RequestMode

    A string to indicate whether the request will use CORS, or will be restricted to same-origin URLs. Sets request's mode.
  + [priority](https://bun.com/reference/globals/BunFetchRequestInit/priority)?: RequestPriority
  + [proxy](https://bun.com/reference/globals/BunFetchRequestInit/proxy)?: string | { headers: [HeadersInit](https://bun.com/reference/bun/HeadersInit); url: string }

    Override http\_proxy or HTTPS\_PROXY This is a custom property that is not part of the Fetch API specification.

    Can be a string URL or an object with `url` and optional `headers`.

    ```
    // String format
    const response = await fetch("http://example.com", {
     proxy: "https://username:password@127.0.0.1:8080"
    });

    // Object format with custom headers sent to the proxy
    const response = await fetch("http://example.com", {
     proxy: {
       url: "https://127.0.0.1:8080",
       headers: {
         "Proxy-Authorization": "Bearer token",
         "X-Custom-Proxy-Header": "value"
       }
     }
    });
    ```

    If a `Proxy-Authorization` header is provided in `proxy.headers`, it takes precedence over credentials parsed from the proxy URL.
  + [redirect](https://bun.com/reference/globals/BunFetchRequestInit/redirect)?: RequestRedirect

    A string indicating whether request follows redirects, results in an error upon encountering a redirect, or returns the redirect (in an opaque fashion). Sets request's redirect.
  + [referrer](https://bun.com/reference/globals/BunFetchRequestInit/referrer)?: string

    A string whose value is a same-origin URL, "about:client", or the empty string, to set request's referrer.
  + [referrerPolicy](https://bun.com/reference/globals/BunFetchRequestInit/referrerPolicy)?: ReferrerPolicy

    A referrer policy to set request's referrerPolicy.
  + [s3](https://bun.com/reference/globals/BunFetchRequestInit/s3)?: [S3Options](https://bun.com/reference/bun/S3Options)

    Override the default S3 options

    ```
    const response = await fetch("s3://bucket/key", {
      s3: {
        accessKeyId: "AKIAIOSFODNN7EXAMPLE",
        secretAccessKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
        region: "us-east-1",
      }
    });
    ```
  + [signal](https://bun.com/reference/globals/BunFetchRequestInit/signal)?: null | [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    An AbortSignal to set request's signal.
  + [tls](https://bun.com/reference/globals/BunFetchRequestInit/tls)?: [BunFetchRequestInitTLS](https://bun.com/reference/globals/BunFetchRequestInitTLS)

    Override the default TLS options
  + [unix](https://bun.com/reference/globals/BunFetchRequestInit/unix)?: string

    Make the request over a Unix socket

    ```
    const response = await fetch("http://example.com", { unix: "/path/to/socket" });
    ```
  + [verbose](https://bun.com/reference/globals/BunFetchRequestInit/verbose)?: boolean

    Log the raw HTTP request & response to stdout. This API may be removed in a future version of Bun without notice. This is a custom property that is not part of the Fetch API specification. It exists mostly as a debugging tool
  + [window](https://bun.com/reference/globals/BunFetchRequestInit/window)?: null

    Can only be null. Used to disassociate request from any Window.
* ### interface [BunFetchRequestInitTLS](https://bun.com/reference/globals/BunFetchRequestInitTLS)

  Extends Bun.TLSOptions with extra properties that are only supported in `fetch(url, {tls: ...})`

  + [ca](https://bun.com/reference/globals/BunFetchRequestInitTLS/ca)?: string | [BunFile](https://bun.com/reference/bun/BunFile) | [BufferSource](https://bun.com/reference/bun/BufferSource) | unknown[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/globals/BunFetchRequestInitTLS/cert)?: string | [BunFile](https://bun.com/reference/bun/BunFile) | [BufferSource](https://bun.com/reference/bun/BufferSource) | unknown[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/globals/BunFetchRequestInitTLS/checkServerIdentity)?: (hostname: string, cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)

    Custom function to check the server identity
  + [ciphers](https://bun.com/reference/globals/BunFetchRequestInitTLS/ciphers)?: string
  + [clientRenegotiationLimit](https://bun.com/reference/globals/BunFetchRequestInitTLS/clientRenegotiationLimit)?: number
  + [clientRenegotiationWindow](https://bun.com/reference/globals/BunFetchRequestInitTLS/clientRenegotiationWindow)?: number
  + [dhParamsFile](https://bun.com/reference/globals/BunFetchRequestInitTLS/dhParamsFile)?: string

    File path to a .pem file custom Diffie Helman parameters
  + [key](https://bun.com/reference/globals/BunFetchRequestInitTLS/key)?: string | [BunFile](https://bun.com/reference/bun/BunFile) | [BufferSource](https://bun.com/reference/bun/BufferSource) | unknown[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [lowMemoryMode](https://bun.com/reference/globals/BunFetchRequestInitTLS/lowMemoryMode)?: boolean

    This sets `OPENSSL_RELEASE_BUFFERS` to 1. It reduces overall performance but saves some memory.
  + [passphrase](https://bun.com/reference/globals/BunFetchRequestInitTLS/passphrase)?: string

    Passphrase for the TLS key
  + [rejectUnauthorized](https://bun.com/reference/globals/BunFetchRequestInitTLS/rejectUnauthorized)?: boolean

    If set to `false`, any certificate is accepted. Default is `$NODE_TLS_REJECT_UNAUTHORIZED` environment variable, or `true` if it is not set.
  + [requestCert](https://bun.com/reference/globals/BunFetchRequestInitTLS/requestCert)?: boolean

    If set to `true`, the server will request a client certificate.

    Default is `false`.
  + [secureOptions](https://bun.com/reference/globals/BunFetchRequestInitTLS/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [serverName](https://bun.com/reference/globals/BunFetchRequestInitTLS/serverName)?: string

    Explicitly set a server name
* ### interface [Console](https://bun.com/reference/globals/Console)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/console)

  + [Console](https://bun.com/reference/globals/Console/Console): [ConsoleConstructor](https://bun.com/reference/globals/console/ConsoleConstructor)
  + [[Symbol.asyncIterator]](https://bun.com/reference/globals/Console/[asyncIterator])(): AsyncIterableIterator<string>;

    Asynchronously read lines from standard input (fd 0)

    ```
    for await (const line of console) {
      console.log(line);
    }
    ```
  + [assert](https://bun.com/reference/globals/Console/assert)(

    condition?: boolean,

    ...data: any[]

    ): void;

    [assert](https://bun.com/reference/globals/Console/assert)(

    value: any,

    message?: string,

    ...optionalParams: any[]

    ): void;

    `console.assert()` writes a message if `value` is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) or omitted. It only writes a message and does not otherwise affect execution. The output always starts with `"Assertion failed"`. If provided, `message` is formatted using [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args).

    If `value` is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy), nothing happens.

    ```
    console.assert(true, 'does nothing');

    console.assert(false, 'Whoops %s work', 'didn\'t');
    // Assertion failed: Whoops didn't work

    console.assert();
    // Assertion failed
    ```

    @param value

    The value tested for being truthy.

    @param message

    All arguments besides `value` are used as error message.
  + [clear](https://bun.com/reference/globals/Console/clear)(): void;

    When `stdout` is a TTY, calling `console.clear()` will attempt to clear the TTY. When `stdout` is not a TTY, this method does nothing.

    The specific operation of `console.clear()` can vary across operating systems and terminal types. For most Linux operating systems, `console.clear()` operates similarly to the `clear` shell command. On Windows, `console.clear()` will clear only the output in the current terminal viewport for the Node.js binary.
  + [count](https://bun.com/reference/globals/Console/count)(

    label?: string

    ): void;

    Maintains an internal counter specific to `label` and outputs to `stdout` the number of times `console.count()` has been called with the given `label`.

    ```
    > console.count()
    default: 1
    undefined
    > console.count('default')
    default: 2
    undefined
    > console.count('abc')
    abc: 1
    undefined
    > console.count('xyz')
    xyz: 1
    undefined
    > console.count('abc')
    abc: 2
    undefined
    > console.count()
    default: 3
    undefined
    >
    ```

    @param label

    The display label for the counter.
  + [countReset](https://bun.com/reference/globals/Console/countReset)(

    label?: string

    ): void;

    Resets the internal counter specific to `label`.

    ```
    > console.count('abc');
    abc: 1
    undefined
    > console.countReset('abc');
    undefined
    > console.count('abc');
    abc: 1
    undefined
    >
    ```

    @param label

    The display label for the counter.
  + [debug](https://bun.com/reference/globals/Console/debug)(

    ...data: any[]

    ): void;

    [debug](https://bun.com/reference/globals/Console/debug)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    The `console.debug()` function is an alias for log.
  + [dir](https://bun.com/reference/globals/Console/dir)(

    item?: any,

    options?: any

    ): void;

    [dir](https://bun.com/reference/globals/Console/dir)(

    obj: any,

    options?: [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

    ): void;

    Uses [`util.inspect()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilinspectobject-options) on `obj` and prints the resulting string to `stdout`. This function bypasses any custom `inspect()` function defined on `obj`.
  + [dirxml](https://bun.com/reference/globals/Console/dirxml)(

    ...data: any[]

    ): void;

    This method calls `console.log()` passing it the arguments received. This method does not produce any XML formatting.
  + [error](https://bun.com/reference/globals/Console/error)(

    ...data: any[]

    ): void;

    Log to stderr in your terminal

    Appears in red

    @param data

    something to display

    [error](https://bun.com/reference/globals/Console/error)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    Prints to `stderr` with newline. Multiple arguments can be passed, with the first used as the primary message and all additional used as substitution values similar to [`printf(3)`](http://man7.org/linux/man-pages/man3/printf.3.html) (the arguments are all passed to [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args)).

    ```
    const code = 5;
    console.error('error #%d', code);
    // Prints: error #5, to stderr
    console.error('error', code);
    // Prints: error 5, to stderr
    ```

    If formatting elements (e.g. `%d`) are not found in the first string then [`util.inspect()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilinspectobject-options) is called on each argument and the resulting string values are concatenated. See [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args) for more information.
  + [group](https://bun.com/reference/globals/Console/group)(

    ...label: any[]

    ): void;

    Increases indentation of subsequent lines by spaces for `groupIndentation` length.

    If one or more `label`s are provided, those are printed first without the additional indentation.
  + [groupCollapsed](https://bun.com/reference/globals/Console/groupCollapsed)(

    ...label: any[]

    ): void;

    An alias for group.
  + [groupEnd](https://bun.com/reference/globals/Console/groupEnd)(): void;

    Decreases indentation of subsequent lines by spaces for `groupIndentation` length.
  + [info](https://bun.com/reference/globals/Console/info)(

    ...data: any[]

    ): void;

    [info](https://bun.com/reference/globals/Console/info)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    The `console.info()` function is an alias for log.
  + [log](https://bun.com/reference/globals/Console/log)(

    ...data: any[]

    ): void;

    [log](https://bun.com/reference/globals/Console/log)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    Prints to `stdout` with newline. Multiple arguments can be passed, with the first used as the primary message and all additional used as substitution values similar to [`printf(3)`](http://man7.org/linux/man-pages/man3/printf.3.html) (the arguments are all passed to [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args)).

    ```
    const count = 5;
    console.log('count: %d', count);
    // Prints: count: 5, to stdout
    console.log('count:', count);
    // Prints: count: 5, to stdout
    ```

    See [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args) for more information.
  + [profile](https://bun.com/reference/globals/Console/profile)(

    label?: string

    ): void;

    This method does not display anything unless used in the inspector. The `console.profile()` method starts a JavaScript CPU profile with an optional label until profileEnd is called. The profile is then added to the Profile panel of the inspector.

    ```
    console.profile('MyLabel');
    // Some code
    console.profileEnd('MyLabel');
    // Adds the profile 'MyLabel' to the Profiles panel of the inspector.
    ```
  + [profileEnd](https://bun.com/reference/globals/Console/profileEnd)(

    label?: string

    ): void;

    This method does not display anything unless used in the inspector. Stops the current JavaScript CPU profiling session if one has been started and prints the report to the Profiles panel of the inspector. See profile for an example.

    If this method is called without a label, the most recently started profile is stopped.
  + [table](https://bun.com/reference/globals/Console/table)(

    tabularData?: any,

    properties?: string[]

    ): void;

    Try to construct a table with the columns of the properties of `tabularData` (or use `properties`) and rows of `tabularData` and log it. Falls back to just logging the argument if it can't be parsed as tabular.

    ```
    // These can't be parsed as tabular data
    console.table(Symbol());
    // Symbol()

    console.table(undefined);
    // undefined

    console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }]);
    // ┌────┬─────┬─────┐
    // │    │  a  │  b  │
    // ├────┼─────┼─────┤
    // │  0 │  1  │ 'Y' │
    // │  1 │ 'Z' │  2  │
    // └────┴─────┴─────┘

    console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }], ['a']);
    // ┌────┬─────┐
    // │    │  a  │
    // ├────┼─────┤
    // │ 0  │  1  │
    // │ 1  │ 'Z' │
    // └────┴─────┘
    ```

    @param properties

    Alternate properties for constructing the table.

    [table](https://bun.com/reference/globals/Console/table)(

    tabularData: any,

    properties?: readonly string[]

    ): void;

    Try to construct a table with the columns of the properties of `tabularData` (or use `properties`) and rows of `tabularData` and log it. Falls back to just logging the argument if it can't be parsed as tabular.

    ```
    // These can't be parsed as tabular data
    console.table(Symbol());
    // Symbol()

    console.table(undefined);
    // undefined

    console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }]);
    // ┌─────────┬─────┬─────┐
    // │ (index) │  a  │  b  │
    // ├─────────┼─────┼─────┤
    // │    0    │  1  │ 'Y' │
    // │    1    │ 'Z' │  2  │
    // └─────────┴─────┴─────┘

    console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }], ['a']);
    // ┌─────────┬─────┐
    // │ (index) │  a  │
    // ├─────────┼─────┤
    // │    0    │  1  │
    // │    1    │ 'Z' │
    // └─────────┴─────┘
    ```

    @param properties

    Alternate properties for constructing the table.
  + [time](https://bun.com/reference/globals/Console/time)(

    label?: string

    ): void;

    Starts a timer that can be used to compute the duration of an operation. Timers are identified by a unique `label`. Use the same `label` when calling timeEnd to stop the timer and output the elapsed time in suitable time units to `stdout`. For example, if the elapsed time is 3869ms, `console.timeEnd()` displays "3.869s".
  + [timeEnd](https://bun.com/reference/globals/Console/timeEnd)(

    label?: string

    ): void;

    Stops a timer that was previously started by calling time and prints the result to `stdout`:

    ```
    console.time('bunch-of-stuff');
    // Do a bunch of stuff.
    console.timeEnd('bunch-of-stuff');
    // Prints: bunch-of-stuff: 225.438ms
    ```
  + [timeLog](https://bun.com/reference/globals/Console/timeLog)(

    label?: string,

    ...data: any[]

    ): void;

    For a timer that was previously started by calling time, prints the elapsed time and other `data` arguments to `stdout`:

    ```
    console.time('process');
    const value = expensiveProcess1(); // Returns 42
    console.timeLog('process', value);
    // Prints "process: 365.227ms 42".
    doExpensiveProcess2(value);
    console.timeEnd('process');
    ```
  + [timeStamp](https://bun.com/reference/globals/Console/timeStamp)(

    label?: string

    ): void;

    This method does not display anything unless used in the inspector. The `console.timeStamp()` method adds an event with the label `'label'` to the Timeline panel of the inspector.
  + [trace](https://bun.com/reference/globals/Console/trace)(

    ...data: any[]

    ): void;

    [trace](https://bun.com/reference/globals/Console/trace)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    Prints to `stderr` the string `'Trace: '`, followed by the [`util.format()`](https://nodejs.org/docs/latest-v24.x/api/util.html#utilformatformat-args) formatted message and stack trace to the current position in the code.

    ```
    console.trace('Show me');
    // Prints: (stack trace will vary based on where trace is called)
    //  Trace: Show me
    //    at repl:2:9
    //    at REPLServer.defaultEval (repl.js:248:27)
    //    at bound (domain.js:287:14)
    //    at REPLServer.runBound [as eval] (domain.js:300:12)
    //    at REPLServer.<anonymous> (repl.js:412:12)
    //    at emitOne (events.js:82:20)
    //    at REPLServer.emit (events.js:169:7)
    //    at REPLServer.Interface._onLine (readline.js:210:10)
    //    at REPLServer.Interface._line (readline.js:549:8)
    //    at REPLServer.Interface._ttyWrite (readline.js:826:14)
    ```
  + [warn](https://bun.com/reference/globals/Console/warn)(

    ...data: any[]

    ): void;

    [warn](https://bun.com/reference/globals/Console/warn)(

    message?: any,

    ...optionalParams: any[]

    ): void;

    The `console.warn()` function is an alias for error.
  + [write](https://bun.com/reference/globals/Console/write)(

    ...data: string | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | ArrayBufferView<ArrayBufferLike>[]

    ): number;

    Write text or bytes to stdout

    Unlike console.log, this does no formatting and doesn't add a newline or spaces between arguments. You can pass it strings or bytes or any combination of the two.

    ```
    console.write("hello world!", "\n"); // "hello world\n"
    ```

    @param data

    The data to write

    @returns

    The number of bytes written

    This function is not available in the browser.
* ### interface [ConsoleOptions](https://bun.com/reference/globals/ConsoleOptions)

  + [colorMode](https://bun.com/reference/globals/ConsoleOptions/colorMode)?: boolean | 'auto'
  + [groupIndentation](https://bun.com/reference/globals/ConsoleOptions/groupIndentation)?: number
  + [ignoreErrors](https://bun.com/reference/globals/ConsoleOptions/ignoreErrors)?: boolean
  + [inspectOptions](https://bun.com/reference/globals/ConsoleOptions/inspectOptions)?: [InspectOptions](https://bun.com/reference/node/util/InspectOptions)
  + [stderr](https://bun.com/reference/globals/ConsoleOptions/stderr)?: [Writable](https://bun.com/reference/node/stream/default/Writable)
  + [stdout](https://bun.com/reference/globals/ConsoleOptions/stdout): [Writable](https://bun.com/reference/node/stream/default/Writable)
* ### interface [CryptoKeyPair](https://bun.com/reference/globals/CryptoKeyPair)

  + [privateKey](https://bun.com/reference/globals/CryptoKeyPair/privateKey): [CryptoKey](https://bun.com/reference/globals/CryptoKey)
  + [publicKey](https://bun.com/reference/globals/CryptoKeyPair/publicKey): [CryptoKey](https://bun.com/reference/globals/CryptoKey)
* ### interface [Dict](https://bun.com/reference/globals/Dict)<T>
* ### interface [ErrnoException](https://bun.com/reference/globals/ErrnoException)

  + [cause](https://bun.com/reference/globals/ErrnoException/cause)?: unknown

    The cause of the error.
  + [code](https://bun.com/reference/globals/ErrnoException/code)?: string
  + [errno](https://bun.com/reference/globals/ErrnoException/errno)?: number
  + [message](https://bun.com/reference/globals/ErrnoException/message): string
  + [name](https://bun.com/reference/globals/ErrnoException/name): string
  + [path](https://bun.com/reference/globals/ErrnoException/path)?: string
  + [stack](https://bun.com/reference/globals/ErrnoException/stack)?: string
  + [syscall](https://bun.com/reference/globals/ErrnoException/syscall)?: string
* ### interface [Error](https://bun.com/reference/globals/Error)

  + [cause](https://bun.com/reference/globals/Error/cause)?: unknown

    The cause of the error.
  + [message](https://bun.com/reference/globals/Error/message): string
  + [name](https://bun.com/reference/globals/Error/name): string
  + [stack](https://bun.com/reference/globals/Error/stack)?: string
* ### interface [ErrorConstructor](https://bun.com/reference/globals/ErrorConstructor)

  + constructor ErrorConstructor(

    message?: string

    ): [Error](https://bun.com/reference/globals/Error);

    constructor ErrorConstructor(

    message?: string,

    options?: [ErrorOptions](https://bun.com/reference/globals/ErrorOptions)

    ): [Error](https://bun.com/reference/globals/Error);
  + readonly [prototype](https://bun.com/reference/globals/ErrorConstructor/prototype): [Error](https://bun.com/reference/globals/Error)
  + [stackTraceLimit](https://bun.com/reference/globals/ErrorConstructor/stackTraceLimit): number

    The `Error.stackTraceLimit` property specifies the number of stack frames collected by a stack trace (whether generated by `new Error().stack` or `Error.captureStackTrace(obj)`).

    The default value is `10` but may be set to any valid JavaScript number. Changes will affect any stack trace captured *after* the value has been changed.

    If set to a non-number value, or set to a negative number, stack traces will not capture any frames.
  + [captureStackTrace](https://bun.com/reference/globals/ErrorConstructor/captureStackTrace)(

    targetObject: object,

    constructorOpt?: Function

    ): void;

    Create .stack property on a target object
  + [isError](https://bun.com/reference/globals/ErrorConstructor/isError)(

    value: unknown

    ): value is [Error](https://bun.com/reference/globals/Error);

    Check if a value is an instance of Error

    @param value

    The value to check

    @returns

    True if the value is an instance of Error, false otherwise
  + [prepareStackTrace](https://bun.com/reference/globals/ErrorConstructor/prepareStackTrace)(

    err: [Error](https://bun.com/reference/globals/Error),

    stackTraces: CallSite[]

    ): any;
* ### interface [ErrorOptions](https://bun.com/reference/globals/ErrorOptions)

  + [cause](https://bun.com/reference/globals/ErrorOptions/cause)?: unknown

    The cause of the error.
* ### interface [EventListener](https://bun.com/reference/globals/EventListener)
* ### interface [EventListenerObject](https://bun.com/reference/globals/EventListenerObject)

  + [handleEvent](https://bun.com/reference/globals/EventListenerObject/handleEvent)(

    object: [Event](https://bun.com/reference/globals/Event)

    ): void;
* ### interface [EventMap](https://bun.com/reference/globals/EventMap)

  + [fetch](https://bun.com/reference/globals/EventMap/fetch): [FetchEvent](https://bun.com/reference/globals/FetchEvent)
  + [message](https://bun.com/reference/globals/EventMap/message): [MessageEvent](https://bun.com/reference/globals/MessageEvent)
  + [messageerror](https://bun.com/reference/globals/EventMap/messageerror): [MessageEvent](https://bun.com/reference/globals/MessageEvent)
* ### interface [EventSource](https://bun.com/reference/globals/EventSource)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource)

  + readonly [CLOSED](https://bun.com/reference/globals/EventSource/CLOSED): 2
  + readonly [CONNECTING](https://bun.com/reference/globals/EventSource/CONNECTING): 0
  + [onerror](https://bun.com/reference/globals/EventSource/onerror): null | (this: [EventSource](https://bun.com/reference/globals/EventSource), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/error_event)
  + [onmessage](https://bun.com/reference/globals/EventSource/onmessage): null | (this: [EventSource](https://bun.com/reference/globals/EventSource), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/message_event)
  + [onopen](https://bun.com/reference/globals/EventSource/onopen): null | (this: [EventSource](https://bun.com/reference/globals/EventSource), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/open_event)
  + readonly [OPEN](https://bun.com/reference/globals/EventSource/OPEN): 1
  + readonly [readyState](https://bun.com/reference/globals/EventSource/readyState): number

    Returns the state of this EventSource object's connection. It can have the values described below.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/readyState)
  + readonly [url](https://bun.com/reference/globals/EventSource/url): string

    Returns the URL providing the event stream.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/url)
  + readonly [withCredentials](https://bun.com/reference/globals/EventSource/withCredentials): boolean

    Returns true if the credentials mode for connection requests to the URL providing the event stream is set to "include", and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/withCredentials)
  + [addEventListener](https://bun.com/reference/globals/EventSource/addEventListener)<K extends keyof EventSourceEventMap>(

    type: K,

    listener: (this: [EventSource](https://bun.com/reference/globals/EventSource), ev: EventSourceEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/EventSource/addEventListener)(

    type: string,

    listener: (this: [EventSource](https://bun.com/reference/globals/EventSource), event: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any,

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

    [addEventListener](https://bun.com/reference/globals/EventSource/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [close](https://bun.com/reference/globals/EventSource/close)(): void;

    Aborts any instances of the fetch algorithm started for this EventSource object, and sets the readyState attribute to CLOSED.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventSource/close)
  + [dispatchEvent](https://bun.com/reference/globals/EventSource/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [removeEventListener](https://bun.com/reference/globals/EventSource/removeEventListener)<K extends keyof EventSourceEventMap>(

    type: K,

    listener: (this: [EventSource](https://bun.com/reference/globals/EventSource), ev: EventSourceEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/EventSource/removeEventListener)(

    type: string,

    listener: (this: [EventSource](https://bun.com/reference/globals/EventSource), event: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/EventSource/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
* ### interface [EventSourceInit](https://bun.com/reference/globals/EventSourceInit)

  + [withCredentials](https://bun.com/reference/globals/EventSourceInit/withCredentials)?: boolean
* ### interface [FetchEvent](https://bun.com/reference/globals/FetchEvent)

  An event which takes place in the DOM.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event)

  + readonly [AT\_TARGET](https://bun.com/reference/globals/FetchEvent/AT_TARGET): 2
  + readonly [bubbles](https://bun.com/reference/globals/FetchEvent/bubbles): boolean

    Returns true or false depending on how event was initialized. True if event goes through its target's ancestors in reverse tree order, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/bubbles)
  + readonly [BUBBLING\_PHASE](https://bun.com/reference/globals/FetchEvent/BUBBLING_PHASE): 3
  + readonly [cancelable](https://bun.com/reference/globals/FetchEvent/cancelable): boolean

    Returns true or false depending on how event was initialized. Its return value does not always carry meaning, but true can indicate that part of the operation during which event was dispatched, can be canceled by invoking the preventDefault() method.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/cancelable)
  + readonly [CAPTURING\_PHASE](https://bun.com/reference/globals/FetchEvent/CAPTURING_PHASE): 1
  + readonly [composed](https://bun.com/reference/globals/FetchEvent/composed): boolean

    Returns true or false depending on how event was initialized. True if event invokes listeners past a ShadowRoot node that is the root of its target, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composed)
  + readonly [currentTarget](https://bun.com/reference/globals/FetchEvent/currentTarget): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object whose event listener's callback is currently being invoked.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/currentTarget)
  + readonly [defaultPrevented](https://bun.com/reference/globals/FetchEvent/defaultPrevented): boolean

    Returns true if preventDefault() was invoked successfully to indicate cancelation, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/defaultPrevented)
  + readonly [eventPhase](https://bun.com/reference/globals/FetchEvent/eventPhase): number

    Returns the event's phase, which is one of NONE, CAPTURING\_PHASE, AT\_TARGET, and BUBBLING\_PHASE.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/eventPhase)
  + readonly [isTrusted](https://bun.com/reference/globals/FetchEvent/isTrusted): boolean

    Returns true if event was dispatched by the user agent, and false otherwise.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/isTrusted)
  + readonly [NONE](https://bun.com/reference/globals/FetchEvent/NONE): 0
  + readonly [request](https://bun.com/reference/globals/FetchEvent/request): [Request](https://bun.com/reference/globals/Request)
  + readonly [target](https://bun.com/reference/globals/FetchEvent/target): null | [EventTarget](https://bun.com/reference/globals/EventTarget)

    Returns the object to which event is dispatched (its target).

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/target)
  + readonly [timeStamp](https://bun.com/reference/globals/FetchEvent/timeStamp): number

    Returns the event's timestamp as the number of milliseconds measured relative to the time origin.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/timeStamp)
  + readonly [type](https://bun.com/reference/globals/FetchEvent/type): string

    Returns the type of event, e.g. "click", "hashchange", or "submit".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/type)
  + readonly [url](https://bun.com/reference/globals/FetchEvent/url): string
  + [composedPath](https://bun.com/reference/globals/FetchEvent/composedPath)(): [EventTarget](https://bun.com/reference/globals/EventTarget)[];

    Returns the invocation target objects of event's path (objects on which listeners will be invoked), except for any nodes in shadow trees of which the shadow root's mode is "closed" that are not reachable from event's currentTarget.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Event/composedPath)
  + [preventDefault](https://bun.com/reference/globals/FetchEvent/preventDefault)(): void;

    Sets the `defaultPrevented` property to `true` if `cancelable` is `true`.
  + [respondWith](https://bun.com/reference/globals/FetchEvent/respondWith)(

    response: [Response](https://bun.com/reference/globals/Response) | Promise<[Response](https://bun.com/reference/globals/Response)>

    ): void;
  + [stopImmediatePropagation](https://bun.com/reference/globals/FetchEvent/stopImmediatePropagation)(): void;

    Stops the invocation of event listeners after the current one completes.
  + [stopPropagation](https://bun.com/reference/globals/FetchEvent/stopPropagation)(): void;

    This is not used in Node.js and is provided purely for completeness.
  + [waitUntil](https://bun.com/reference/globals/FetchEvent/waitUntil)(

    promise: Promise<any>

    ): void;
* ### interface [ImportMeta](https://bun.com/reference/globals/ImportMeta)

  The type of `import.meta`.

  If you need to declare that a given property exists on `import.meta`, this type may be augmented via interface merging.

  + readonly [dir](https://bun.com/reference/globals/ImportMeta/dir): string

    Absolute path to the directory containing the source file.

    Does not have a trailing slash
  + [dirname](https://bun.com/reference/globals/ImportMeta/dirname): string

    Alias of `import.meta.dir`. Exists for Node.js compatibility
  + readonly [env](https://bun.com/reference/globals/ImportMeta/env): [Env](https://bun.com/reference/bun/Env) & ProcessEnv & [ImportMetaEnv](https://bun.com/reference/globals/ImportMetaEnv)

    The environment variables of the process

    ```
    import.meta.env === process.env
    ```
  + readonly [file](https://bun.com/reference/globals/ImportMeta/file): string

    Filename of the source file
  + [filename](https://bun.com/reference/globals/ImportMeta/filename): string

    Alias of `import.meta.path`. Exists for Node.js compatibility
  + [hot](https://bun.com/reference/globals/ImportMeta/hot): { data: any; accept(): void; decline; dispose(cb: (data: any) => void | Promise<void>): void; off(event: [HMREvent](https://bun.com/reference/bun/HMREvent), callback: () => void): void; on(event: [HMREvent](https://bun.com/reference/bun/HMREvent), callback: () => void): void }

    Hot module replacement APIs. This value is `undefined` in production and can be used in an `if` statement to check if HMR APIs are available

    ```
    if (import.meta.hot) {
      // HMR APIs are available
    }
    ```

    However, this check is usually not needed as Bun will dead-code-eliminate calls to all of the HMR APIs in production builds.

    https://bun.com/docs/bundler/hmr
  + [main](https://bun.com/reference/globals/ImportMeta/main): boolean

    Did the current file start the process?

    ```
    if (import.meta.main) {
     console.log("I started the process!");
    }
    ```
  + readonly [path](https://bun.com/reference/globals/ImportMeta/path): string

    Absolute path to the source file
  + [require](https://bun.com/reference/globals/ImportMeta/require): Require

    Load a CommonJS module within an ES Module. Bun's transpiler rewrites all calls to `require` with `import.meta.require` when transpiling ES Modules for the runtime.

    Warning: **This API is not stable** and may change or be removed in the future. Use at your own risk.
  + [url](https://bun.com/reference/globals/ImportMeta/url): string

    `file://` url string for the current module.

    ```
    console.log(import.meta.url);
    "file:///Users/me/projects/my-app/src/my-app.ts"
    ```
  + [resolve](https://bun.com/reference/globals/ImportMeta/resolve)(

    specifier: string

    ): string;

    [resolve](https://bun.com/reference/globals/ImportMeta/resolve)(

    specifier: string,

    parent?: string | [URL](https://bun.com/reference/node/url/URL)

    ): string;

    `import.meta.resolve` is a module-relative resolution function scoped to each module, returning the URL string.

    ```
    const dependencyAsset = import.meta.resolve('component-lib/asset.css');
    // file:///app/node_modules/component-lib/asset.css
    import.meta.resolve('./dep.js');
    // file:///app/dep.js
    ```

    All features of the Node.js module resolution are supported. Dependency resolutions are subject to the permitted exports resolutions within the package.

    **Caveats**:

    - This can result in synchronous file-system operations, which can impact performance similarly to `require.resolve`.
    - This feature is not available within custom loaders (it would create a deadlock).

    @param specifier

    The module specifier to resolve relative to the current module.

    @param parent

    An optional absolute parent module URL to resolve from. **Default:** `import.meta.url`

    @returns

    The absolute URL string that the specifier would resolve to.
* ### interface [ImportMetaEnv](https://bun.com/reference/globals/ImportMetaEnv)
* ### interface [Position](https://bun.com/reference/globals/Position)

  + [column](https://bun.com/reference/globals/Position/column): number
  + [file](https://bun.com/reference/globals/Position/file): string
  + [length](https://bun.com/reference/globals/Position/length): number
  + [line](https://bun.com/reference/globals/Position/line): number
  + [lineText](https://bun.com/reference/globals/Position/lineText): string
  + [namespace](https://bun.com/reference/globals/Position/namespace): string
  + [offset](https://bun.com/reference/globals/Position/offset): number
* ### interface [PromiseConstructor](https://bun.com/reference/globals/PromiseConstructor)

  Represents the completion of an asynchronous operation

  + constructor PromiseConstructor<T>(

    executor: (resolve: (value: T | PromiseLike<T>) => void, reject: (reason?: any) => void) => void

    ): Promise<T>;

    Creates a new Promise.

    @param executor

    A callback used to initialize the promise. This callback is passed two arguments: a resolve callback used to resolve the promise with a value or the result of another promise, and a reject callback used to reject the promise with a provided reason or error.
  + readonly [[Symbol.species]](https://bun.com/reference/globals/PromiseConstructor/[species]): [PromiseConstructor](https://bun.com/reference/globals/PromiseConstructor)
  + readonly [prototype](https://bun.com/reference/globals/PromiseConstructor/prototype): Promise<any>

    A reference to the prototype.
  + [all](https://bun.com/reference/globals/PromiseConstructor/all)<T>(

    values: Iterable<T | PromiseLike<T>>

    ): Promise<Awaited<T>[]>;

    Creates a Promise that is resolved with an array of results when all of the provided Promises resolve, or rejected when any Promise is rejected.

    @param values

    An iterable of Promises.

    @returns

    A new Promise.

    [all](https://bun.com/reference/globals/PromiseConstructor/all)<T extends [] | readonly unknown[]>(

    values: T

    ): Promise<{ [K in string | number | symbol]: Awaited<T[P<P>]> }>;

    Creates a Promise that is resolved with an array of results when all of the provided Promises resolve, or rejected when any Promise is rejected.

    @param values

    An array of Promises.

    @returns

    A new Promise.
  + [allSettled](https://bun.com/reference/globals/PromiseConstructor/allSettled)<T extends [] | readonly unknown[]>(

    values: T

    ): Promise<{ [K in string | number | symbol]: PromiseSettledResult<Awaited<T[P<P>]>> }>;

    Creates a Promise that is resolved with an array of results when all of the provided Promises resolve or reject.

    @param values

    An array of Promises.

    @returns

    A new Promise.

    [allSettled](https://bun.com/reference/globals/PromiseConstructor/allSettled)<T>(

    values: Iterable<T | PromiseLike<T>>

    ): Promise<PromiseSettledResult<Awaited<T>>[]>;

    Creates a Promise that is resolved with an array of results when all of the provided Promises resolve or reject.

    @param values

    An array of Promises.

    @returns

    A new Promise.
  + [any](https://bun.com/reference/globals/PromiseConstructor/any)<T extends [] | readonly unknown[]>(

    values: T

    ): Promise<Awaited<T[number]>>;

    The any function returns a promise that is fulfilled by the first given promise to be fulfilled, or rejected with an AggregateError containing an array of rejection reasons if all of the given promises are rejected. It resolves all elements of the passed iterable to promises as it runs this algorithm.

    @param values

    An array or iterable of Promises.

    @returns

    A new Promise.

    [any](https://bun.com/reference/globals/PromiseConstructor/any)<T>(

    values: Iterable<T | PromiseLike<T>>

    ): Promise<Awaited<T>>;

    The any function returns a promise that is fulfilled by the first given promise to be fulfilled, or rejected with an AggregateError containing an array of rejection reasons if all of the given promises are rejected. It resolves all elements of the passed iterable to promises as it runs this algorithm.

    @param values

    An array or iterable of Promises.

    @returns

    A new Promise.
  + [race](https://bun.com/reference/globals/PromiseConstructor/race)<T>(

    values: Iterable<T | PromiseLike<T>>

    ): Promise<Awaited<T>>;

    Creates a Promise that is resolved or rejected when any of the provided Promises are resolved or rejected.

    @param values

    An iterable of Promises.

    @returns

    A new Promise.

    [race](https://bun.com/reference/globals/PromiseConstructor/race)<T extends [] | readonly unknown[]>(

    values: T

    ): Promise<Awaited<T[number]>>;

    Creates a Promise that is resolved or rejected when any of the provided Promises are resolved or rejected.

    @param values

    An array of Promises.

    @returns

    A new Promise.
  + [reject](https://bun.com/reference/globals/PromiseConstructor/reject)<T = never>(

    reason?: any

    ): Promise<T>;

    Creates a new rejected promise for the provided reason.

    @param reason

    The reason the promise was rejected.

    @returns

    A new rejected Promise.
  + [resolve](https://bun.com/reference/globals/PromiseConstructor/resolve)(): Promise<void>;

    Creates a new resolved promise.

    @returns

    A resolved promise.

    [resolve](https://bun.com/reference/globals/PromiseConstructor/resolve)<T>(

    value: T

    ): Promise<Awaited<T>>;

    Creates a new resolved promise for the provided value.

    @param value

    A promise.

    @returns

    A promise whose internal state matches the provided promise.

    [resolve](https://bun.com/reference/globals/PromiseConstructor/resolve)<T>(

    value: T | PromiseLike<T>

    ): Promise<Awaited<T>>;

    Creates a new resolved promise for the provided value.

    @param value

    A promise.

    @returns

    A promise whose internal state matches the provided promise.
  + [try](https://bun.com/reference/globals/PromiseConstructor/try)<T, U extends unknown[]>(

    callbackFn: (...args: U) => T | PromiseLike<T>,

    ...args: U

    ): Promise<Awaited<T>>;

    Takes a callback of any kind (returns or throws, synchronously or asynchronously) and wraps its result in a Promise.

    @param callbackFn

    A function that is called synchronously. It can do anything: either return a value, throw an error, or return a promise.

    @param args

    Additional arguments, that will be passed to the callback.

    @returns

    A Promise that is:

    - Already fulfilled, if the callback synchronously returns a value.
    - Already rejected, if the callback synchronously throws an error.
    - Asynchronously fulfilled or rejected, if the callback returns a promise.

    [try](https://bun.com/reference/globals/PromiseConstructor/try)<T, A extends any[] = []>(

    fn: (...args: A) => T | PromiseLike<T>,

    ...args: A

    ): Promise<T>;

    Try to run a function and return the result. If the function throws, return the result of the `catch` function.

    @param fn

    The function to run

    @param args

    The arguments to pass to the function. This is similar to `setTimeout` and avoids the extra closure.

    @returns

    The result of the function or the result of the `catch` function
  + [withResolvers](https://bun.com/reference/globals/PromiseConstructor/withResolvers)<T>(): PromiseWithResolvers<T>;

    Creates a new Promise and returns it in an object, along with its resolve and reject functions.

    @returns

    An object with the properties `promise`, `resolve`, and `reject`.

    ```
    const { promise, resolve, reject } = Promise.withResolvers<T>();
    ```

    [withResolvers](https://bun.com/reference/globals/PromiseConstructor/withResolvers)<T>(): { promise: Promise<T>; reject: (reason?: any) => void; resolve: (value?: T | PromiseLike<T>) => void };

    Create a deferred promise, with exposed `resolve` and `reject` methods which can be called separately.

    This is useful when you want to return a Promise and have code outside the Promise resolve or reject it.

    ```
    const { promise, resolve, reject } = Promise.withResolvers();

    setTimeout(() => {
     resolve("Hello world!");
    }, 1000);

    await promise; // "Hello world!"
    ```
* ### interface [QueuingStrategy](https://bun.com/reference/globals/QueuingStrategy)<T = any>

  + [highWaterMark](https://bun.com/reference/globals/QueuingStrategy/highWaterMark)?: number
  + [size](https://bun.com/reference/globals/QueuingStrategy/size)?: [QueuingStrategySize](https://bun.com/reference/globals/QueuingStrategySize)<T>
* ### interface [QueuingStrategyInit](https://bun.com/reference/globals/QueuingStrategyInit)

  + [highWaterMark](https://bun.com/reference/globals/QueuingStrategyInit/highWaterMark): number

    Creates a new ByteLengthQueuingStrategy with the provided high water mark.

    Note that the provided high water mark will not be validated ahead of time. Instead, if it is negative, NaN, or not a number, the resulting ByteLengthQueuingStrategy will cause the corresponding stream constructor to throw.
* ### interface [QueuingStrategySize](https://bun.com/reference/globals/QueuingStrategySize)<T = any>
* ### interface [ReadableStreamDefaultReadDoneResult](https://bun.com/reference/globals/ReadableStreamDefaultReadDoneResult)

  + [done](https://bun.com/reference/globals/ReadableStreamDefaultReadDoneResult/done): true
  + [value](https://bun.com/reference/globals/ReadableStreamDefaultReadDoneResult/value)?: undefined
* ### interface [ReadableStreamDefaultReadValueResult](https://bun.com/reference/globals/ReadableStreamDefaultReadValueResult)<T>

  + [done](https://bun.com/reference/globals/ReadableStreamDefaultReadValueResult/done): false
  + [value](https://bun.com/reference/globals/ReadableStreamDefaultReadValueResult/value): T
* ### interface [ReadableStreamDirectController](https://bun.com/reference/globals/ReadableStreamDirectController)

  + [close](https://bun.com/reference/globals/ReadableStreamDirectController/close)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): void;
  + [end](https://bun.com/reference/globals/ReadableStreamDirectController/end)(): number | Promise<number>;
  + [flush](https://bun.com/reference/globals/ReadableStreamDirectController/flush)(): number | Promise<number>;
  + [start](https://bun.com/reference/globals/ReadableStreamDirectController/start)(): void;
  + [write](https://bun.com/reference/globals/ReadableStreamDirectController/write)(

    data: string | [BufferSource](https://bun.com/reference/bun/BufferSource)

    ): number | Promise<number>;
* ### interface [ReadableStreamGenericReader](https://bun.com/reference/globals/ReadableStreamGenericReader)

  + readonly [closed](https://bun.com/reference/globals/ReadableStreamGenericReader/closed): Promise<void>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/closed)
  + [cancel](https://bun.com/reference/globals/ReadableStreamGenericReader/cancel)(

    reason?: any

    ): Promise<void>;
* ### interface [ReadableWritablePair](https://bun.com/reference/globals/ReadableWritablePair)<R = any, W = any>

  + [readable](https://bun.com/reference/globals/ReadableWritablePair/readable): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<R>
  + [writable](https://bun.com/reference/globals/ReadableWritablePair/writable): [WritableStream](https://bun.com/reference/globals/WritableStream)<W>

    Provides a convenient, chainable way of piping this readable stream through a transform stream (or any other { writable, readable } pair). It simply pipes the stream into the writable side of the supplied pair, and returns the readable side for further use.

    Piping a stream will lock it for the duration of the pipe, preventing any other consumer from acquiring a reader.
* ### interface [ReadOnlyDict](https://bun.com/reference/globals/ReadOnlyDict)<T>
* ### interface [RegExpConstructor](https://bun.com/reference/globals/RegExpConstructor)

  + constructor RegExpConstructor(

    pattern: string | RegExp

    ): RegExp;

    constructor RegExpConstructor(

    pattern: string,

    flags?: string

    ): RegExp;

    constructor RegExpConstructor(

    pattern: string | RegExp,

    flags?: string

    ): RegExp;
  + readonly [[Symbol.species]](https://bun.com/reference/globals/RegExpConstructor/[species]): [RegExpConstructor](https://bun.com/reference/globals/RegExpConstructor)
  + readonly [prototype](https://bun.com/reference/globals/RegExpConstructor/prototype): RegExp
  + [escape](https://bun.com/reference/globals/RegExpConstructor/escape)(

    string: string

    ): string;

    Escapes any potential regex syntax characters in a string, and returns a new string that can be safely used as a literal pattern for the RegExp() constructor.

    [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/escape)

    ```
    const re = new RegExp(RegExp.escape("foo.bar"));
    re.test("foo.bar"); // true
    re.test("foo!bar"); // false
    ```
* ### interface [RequestInit](https://bun.com/reference/globals/RequestInit)

  + [body](https://bun.com/reference/globals/RequestInit/body)?: null | BodyInit

    A BodyInit object or null to set request's body.
  + [cache](https://bun.com/reference/globals/RequestInit/cache)?: RequestCache

    A string indicating how the request will interact with the browser's cache to set request's cache.
  + [credentials](https://bun.com/reference/globals/RequestInit/credentials)?: RequestCredentials

    A string indicating whether credentials will be sent with the request always, never, or only when sent to a same-origin URL. Sets request's credentials.
  + [headers](https://bun.com/reference/globals/RequestInit/headers)?: HeadersInit

    A Headers object, an object literal, or an array of two-item arrays to set request's headers.
  + [integrity](https://bun.com/reference/globals/RequestInit/integrity)?: string

    A cryptographic hash of the resource to be fetched by request. Sets request's integrity.
  + [keepalive](https://bun.com/reference/globals/RequestInit/keepalive)?: boolean

    A boolean to set request's keepalive.
  + [method](https://bun.com/reference/globals/RequestInit/method)?: string

    A string to set request's method.
  + [mode](https://bun.com/reference/globals/RequestInit/mode)?: RequestMode

    A string to indicate whether the request will use CORS, or will be restricted to same-origin URLs. Sets request's mode.
  + [priority](https://bun.com/reference/globals/RequestInit/priority)?: RequestPriority
  + [redirect](https://bun.com/reference/globals/RequestInit/redirect)?: RequestRedirect

    A string indicating whether request follows redirects, results in an error upon encountering a redirect, or returns the redirect (in an opaque fashion). Sets request's redirect.
  + [referrer](https://bun.com/reference/globals/RequestInit/referrer)?: string

    A string whose value is a same-origin URL, "about:client", or the empty string, to set request's referrer.
  + [referrerPolicy](https://bun.com/reference/globals/RequestInit/referrerPolicy)?: ReferrerPolicy

    A referrer policy to set request's referrerPolicy.
  + [signal](https://bun.com/reference/globals/RequestInit/signal)?: null | [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    An AbortSignal to set request's signal.
  + [window](https://bun.com/reference/globals/RequestInit/window)?: null

    Can only be null. Used to disassociate request from any Window.
* ### interface [ResponseInit](https://bun.com/reference/globals/ResponseInit)

  + [headers](https://bun.com/reference/globals/ResponseInit/headers)?: HeadersInit
  + [status](https://bun.com/reference/globals/ResponseInit/status)?: number
  + [statusText](https://bun.com/reference/globals/ResponseInit/statusText)?: string
* ### interface [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer)

  + readonly [[Symbol.species]](https://bun.com/reference/globals/SharedArrayBuffer/[species]): [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer)
  + readonly [[Symbol.toStringTag]](https://bun.com/reference/globals/SharedArrayBuffer/[toStringTag]): 'SharedArrayBuffer'
  + readonly [byteLength](https://bun.com/reference/globals/SharedArrayBuffer/byteLength): number

    Read-only. The length of the ArrayBuffer (in bytes).
  + get growable
  + get maxByteLength
  + [grow](https://bun.com/reference/globals/SharedArrayBuffer/grow)(

    newByteLength?: number

    ): void;

    Grows the SharedArrayBuffer to the specified size (in bytes).

    [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer/grow)

    [grow](https://bun.com/reference/globals/SharedArrayBuffer/grow)(

    size: number

    ): [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer);

    Grow the SharedArrayBuffer in-place.
  + [slice](https://bun.com/reference/globals/SharedArrayBuffer/slice)(

    begin?: number,

    end?: number

    ): [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer);

    Returns a section of an SharedArrayBuffer.
* ### interface [StreamPipeOptions](https://bun.com/reference/globals/StreamPipeOptions)

  + [preventAbort](https://bun.com/reference/globals/StreamPipeOptions/preventAbort)?: boolean
  + [preventCancel](https://bun.com/reference/globals/StreamPipeOptions/preventCancel)?: boolean
  + [preventClose](https://bun.com/reference/globals/StreamPipeOptions/preventClose)?: boolean

    Pipes this readable stream to a given writable stream destination. The way in which the piping process behaves under various error conditions can be customized with a number of passed options. It returns a promise that fulfills when the piping process completes successfully, or rejects if any errors were encountered.

    Piping a stream will lock it for the duration of the pipe, preventing any other consumer from acquiring a reader.

    Errors and closures of the source and destination streams propagate as follows:

    An error in this source readable stream will abort destination, unless preventAbort is truthy. The returned promise will be rejected with the source's error, or with any error that occurs during aborting the destination.

    An error in destination will cancel this source readable stream, unless preventCancel is truthy. The returned promise will be rejected with the destination's error, or with any error that occurs during canceling the source.

    When this source readable stream closes, destination will be closed, unless preventClose is truthy. The returned promise will be fulfilled once this process completes, unless an error is encountered while closing the destination, in which case it will be rejected with that error.

    If destination starts out closed or closing, this source readable stream will be canceled, unless preventCancel is true. The returned promise will be rejected with an error indicating piping to a closed stream failed, or with any error that occurs during canceling the source.

    The signal option can be set to an AbortSignal to allow aborting an ongoing pipe operation via the corresponding AbortController. In this case, this source readable stream will be canceled, and destination aborted, unless the respective options preventCancel or preventAbort are set.
  + [signal](https://bun.com/reference/globals/StreamPipeOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
* ### interface [Timer](https://bun.com/reference/globals/Timer)

  + [[Symbol.toPrimitive]](https://bun.com/reference/globals/Timer/[toPrimitive])(): number;
  + [hasRef](https://bun.com/reference/globals/Timer/hasRef)(): boolean;
  + [ref](https://bun.com/reference/globals/Timer/ref)(): [Timer](https://bun.com/reference/globals/Timer);
  + [refresh](https://bun.com/reference/globals/Timer/refresh)(): [Timer](https://bun.com/reference/globals/Timer);
  + [unref](https://bun.com/reference/globals/Timer/unref)(): [Timer](https://bun.com/reference/globals/Timer);
* ### interface [Transformer](https://bun.com/reference/globals/Transformer)<I = any, O = any>

  + [flush](https://bun.com/reference/globals/Transformer/flush)?: TransformerFlushCallback<O>
  + [readableType](https://bun.com/reference/globals/Transformer/readableType)?: undefined
  + [start](https://bun.com/reference/globals/Transformer/start)?: TransformerStartCallback<O>
  + [transform](https://bun.com/reference/globals/Transformer/transform)?: TransformerTransformCallback<I, O>
  + [writableType](https://bun.com/reference/globals/Transformer/writableType)?: undefined
* ### interface [Uint8ArrayConstructor](https://bun.com/reference/globals/Uint8ArrayConstructor)

  + constructor Uint8ArrayConstructor(

    length: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    constructor Uint8ArrayConstructor(

    array: ArrayLike<number>

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    constructor Uint8ArrayConstructor<TArrayBuffer extends ArrayBufferLike = [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>(

    buffer: TArrayBuffer,

    byteOffset?: number,

    length?: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<TArrayBuffer>;

    constructor Uint8ArrayConstructor(

    buffer: [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer),

    byteOffset?: number,

    length?: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    constructor Uint8ArrayConstructor(

    array: [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | ArrayLike<number>

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    constructor Uint8ArrayConstructor(

    elements: Iterable<number>

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    constructor (): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;
  + readonly [BYTES\_PER\_ELEMENT](https://bun.com/reference/globals/Uint8ArrayConstructor/BYTES_PER_ELEMENT): number

    The size in bytes of each element in the array.
  + readonly [prototype](https://bun.com/reference/globals/Uint8ArrayConstructor/prototype): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>
  + [from](https://bun.com/reference/globals/Uint8ArrayConstructor/from)(

    arrayLike: ArrayLike<number>

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Creates an array from an array-like or iterable object.

    @param arrayLike

    An array-like object to convert to an array.

    [from](https://bun.com/reference/globals/Uint8ArrayConstructor/from)<T>(

    arrayLike: ArrayLike<T>,

    mapfn: (v: T, k: number) => number,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Creates an array from an array-like or iterable object.

    @param arrayLike

    An array-like object to convert to an array.

    @param mapfn

    A mapping function to call on every element of the array.

    @param thisArg

    Value of 'this' used to invoke the mapfn.

    [from](https://bun.com/reference/globals/Uint8ArrayConstructor/from)(

    elements: Iterable<number>

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Creates an array from an array-like or iterable object.

    @param elements

    An iterable object to convert to an array.

    [from](https://bun.com/reference/globals/Uint8ArrayConstructor/from)<T>(

    elements: Iterable<T>,

    mapfn?: (v: T, k: number) => number,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Creates an array from an array-like or iterable object.

    @param elements

    An iterable object to convert to an array.

    @param mapfn

    A mapping function to call on every element of the array.

    @param thisArg

    Value of 'this' used to invoke the mapfn.
  + [fromBase64](https://bun.com/reference/globals/Uint8ArrayConstructor/fromBase64)(

    base64: string,

    options?: { alphabet: 'base64' | 'base64url'; lastChunkHandling: 'loose' | 'strict' | 'stop-before-partial' }

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Create a new Uint8Array from a base64 encoded string

    @param base64

    The base64 encoded string to convert to a Uint8Array

    @param options

    Optional options for decoding the base64 string

    @returns

    A new Uint8Array containing the decoded data
  + [fromHex](https://bun.com/reference/globals/Uint8ArrayConstructor/fromHex)(

    hex: string

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Create a new Uint8Array from a hex encoded string

    @param hex

    The hex encoded string to convert to a Uint8Array

    @returns

    A new Uint8Array containing the decoded data
  + [of](https://bun.com/reference/globals/Uint8ArrayConstructor/of)(

    ...items: number[]

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns a new array from a set of elements.

    @param items

    A set of elements to include in the new array object.
* ### interface [WebSocket](https://bun.com/reference/globals/WebSocket)

  Provides the API for creating and managing a WebSocket connection to a server, as well as for sending and receiving data on the connection.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket)

  + [binaryType](https://bun.com/reference/globals/WebSocket/binaryType): BinaryType

    Returns a string that indicates how binary data from the WebSocket object is exposed to scripts:

    Can be set, to change how binary data is returned. The default is "blob".

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/binaryType)
  + readonly [bufferedAmount](https://bun.com/reference/globals/WebSocket/bufferedAmount): number

    Returns the number of bytes of application data (UTF-8 text and binary data) that have been queued using send() but not yet been transmitted to the network.

    If the WebSocket connection is closed, this attribute's value will only increase with each call to the send() method. (The number does not reset to zero once the connection closes.)

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/bufferedAmount)
  + readonly [CLOSED](https://bun.com/reference/globals/WebSocket/CLOSED): 3
  + readonly [CLOSING](https://bun.com/reference/globals/WebSocket/CLOSING): 2
  + readonly [CONNECTING](https://bun.com/reference/globals/WebSocket/CONNECTING): 0
  + readonly [extensions](https://bun.com/reference/globals/WebSocket/extensions): string

    Returns the extensions selected by the server, if any.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/extensions)
  + [onclose](https://bun.com/reference/globals/WebSocket/onclose): null | (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: [CloseEvent](https://bun.com/reference/globals/CloseEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/close_event)
  + [onerror](https://bun.com/reference/globals/WebSocket/onerror): null | (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/error_event)
  + [onmessage](https://bun.com/reference/globals/WebSocket/onmessage): null | (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/message_event)
  + [onopen](https://bun.com/reference/globals/WebSocket/onopen): null | (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: [Event](https://bun.com/reference/globals/Event)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/open_event)
  + readonly [OPEN](https://bun.com/reference/globals/WebSocket/OPEN): 1
  + readonly [readyState](https://bun.com/reference/globals/WebSocket/readyState): number

    Returns the state of the WebSocket object's connection. It can have the values described below.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/readyState)
  + readonly [url](https://bun.com/reference/globals/WebSocket/url): string

    Returns the URL that was used to establish the WebSocket connection.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/url)
  + [addEventListener](https://bun.com/reference/globals/WebSocket/addEventListener)<K extends keyof WebSocketEventMap>(

    type: K,

    listener: (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: WebSocketEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/WebSocket/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [close](https://bun.com/reference/globals/WebSocket/close)(

    code?: number,

    reason?: string

    ): void;

    Closes the WebSocket connection, optionally using code as the the WebSocket connection close code and reason as the the WebSocket connection close reason.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/close)
  + [dispatchEvent](https://bun.com/reference/globals/WebSocket/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [removeEventListener](https://bun.com/reference/globals/WebSocket/removeEventListener)<K extends keyof WebSocketEventMap>(

    type: K,

    listener: (this: [WebSocket](https://bun.com/reference/globals/WebSocket), ev: WebSocketEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/WebSocket/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
  + [send](https://bun.com/reference/globals/WebSocket/send)(

    data: string | ArrayBufferLike | [Blob](https://bun.com/reference/globals/Blob) | ArrayBufferView<ArrayBufferLike>

    ): void;

    Transmits data using the WebSocket connection. data can be a string, a Blob, an ArrayBuffer, or an ArrayBufferView.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/WebSocket/send)
* ### interface [Worker](https://bun.com/reference/globals/Worker)

  This Web Workers API interface represents a background task that can be easily created and can send messages back to its creator. Creating a worker is as simple as calling the Worker() constructor and specifying a script to be run in the worker thread.

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/Worker)

  + [onerror](https://bun.com/reference/globals/Worker/onerror): null | (this: AbstractWorker, ev: [ErrorEvent](https://bun.com/reference/globals/ErrorEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ServiceWorker/error_event)
  + [onmessage](https://bun.com/reference/globals/Worker/onmessage): null | (this: [Worker](https://bun.com/reference/globals/Worker), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DedicatedWorkerGlobalScope/message_event)
  + [onmessageerror](https://bun.com/reference/globals/Worker/onmessageerror): null | (this: [Worker](https://bun.com/reference/globals/Worker), ev: [MessageEvent](https://bun.com/reference/globals/MessageEvent)) => any

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/DedicatedWorkerGlobalScope/messageerror_event)
  + [addEventListener](https://bun.com/reference/globals/Worker/addEventListener)<K extends keyof WorkerEventMap>(

    type: K,

    listener: (this: [Worker](https://bun.com/reference/globals/Worker), ev: WorkerEventMap[K]) => any,

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

    [addEventListener](https://bun.com/reference/globals/Worker/addEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

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
  + [dispatchEvent](https://bun.com/reference/globals/Worker/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [postMessage](https://bun.com/reference/globals/Worker/postMessage)(

    message: any,

    transfer: Transferable[]

    ): void;

    Clones message and transmits it to worker's global environment. transfer can be passed as a list of objects that are to be transferred rather than cloned.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Worker/postMessage)

    [postMessage](https://bun.com/reference/globals/Worker/postMessage)(

    message: any,

    options?: StructuredSerializeOptions

    ): void;
  + [removeEventListener](https://bun.com/reference/globals/Worker/removeEventListener)<K extends keyof WorkerEventMap>(

    type: K,

    listener: (this: [Worker](https://bun.com/reference/globals/Worker), ev: WorkerEventMap[K]) => any,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/globals/Worker/removeEventListener)(

    type: string,

    listener: EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)
  + [terminate](https://bun.com/reference/globals/Worker/terminate)(): void;

    Aborts worker's associated global environment.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/Worker/terminate)
* ### interface [WorkerOptions](https://bun.com/reference/globals/WorkerOptions)

  Bun's Web Worker constructor supports some extra options on top of the API browsers have.

  + [argv](https://bun.com/reference/globals/WorkerOptions/argv)?: any[]

    List of arguments which would be stringified and appended to `Bun.argv` / `process.argv` in the worker. This is mostly similar to the `data` but the values will be available on the global `Bun.argv` as if they were passed as CLI options to the script.
  + [credentials](https://bun.com/reference/globals/WorkerOptions/credentials)?: RequestCredentials

    In Bun, this does nothing.
  + [env](https://bun.com/reference/globals/WorkerOptions/env)?: Record<string, string> | typeof [SHARE\_ENV](https://bun.com/reference/node/worker_threads/SHARE_ENV)

    If set, specifies the initial value of process.env inside the Worker thread. As a special value, worker.SHARE\_ENV may be used to specify that the parent thread and the child thread should share their environment variables; in that case, changes to one thread's process.env object affect the other thread as well. Default: process.env.
  + [name](https://bun.com/reference/globals/WorkerOptions/name)?: string

    A string specifying an identifying name for the DedicatedWorkerGlobalScope representing the scope of the worker, which is mainly useful for debugging purposes.
  + [preload](https://bun.com/reference/globals/WorkerOptions/preload)?: string | string[]

    An array of module specifiers to preload in the worker.

    These modules load before the worker's entry point is executed.

    Equivalent to passing the `--preload` CLI argument, but only for this Worker.
  + [ref](https://bun.com/reference/globals/WorkerOptions/ref)?: boolean

    When `true`, the worker will keep the parent thread alive until the worker is terminated or `unref`'d. When `false`, the worker will not keep the parent thread alive.

    By default, this is `false`.
  + [smol](https://bun.com/reference/globals/WorkerOptions/smol)?: boolean

    Use less memory, but make the worker slower.

    Internally, this sets the heap size configuration in JavaScriptCore to be the small heap instead of the large heap.
  + [type](https://bun.com/reference/globals/WorkerOptions/type)?: WorkerType

    In Bun, this does nothing.