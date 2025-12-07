---
url: https://bun.com/reference/node/inspector
title: Node.js inspector module | API Reference | Bun
source_domain: bun.com
---

# Node.js inspector module | API Reference | Bun

Node.js module

# [inspector](https://bun.com/reference/node/inspector)

Not implemented in Bun

Not implemented. Debugging is typically done via standard debugger protocols (like Chrome DevTools Protocol) connected to the Bun process itself, not via this module.

* ### namespace [Network](https://bun.com/reference/node/inspector/Network)

  + ### interface [DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)

    - [data](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType/data)?: string

      Data that was received.
    - [dataLength](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType/dataLength): number

      Data chunk length.
    - [encodedDataLength](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType/encodedDataLength): number

      Actual bytes received (might be less than dataLength for compressed encodings).
    - [requestId](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType/requestId): string

      Request identifier.
    - [timestamp](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType/timestamp): number

      Timestamp.
  + ### interface [GetRequestPostDataParameterType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataParameterType)

    - [requestId](https://bun.com/reference/node/inspector/Network/GetRequestPostDataParameterType/requestId): string

      Identifier of the network request to get content for.
  + ### interface [GetRequestPostDataReturnType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataReturnType)

    - [postData](https://bun.com/reference/node/inspector/Network/GetRequestPostDataReturnType/postData): string

      Request body string, omitting files from multipart requests
  + ### interface [GetResponseBodyParameterType](https://bun.com/reference/node/inspector/Network/GetResponseBodyParameterType)

    - [requestId](https://bun.com/reference/node/inspector/Network/GetResponseBodyParameterType/requestId): string

      Identifier of the network request to get content for.
  + ### interface [GetResponseBodyReturnType](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType)

    - [base64Encoded](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType/base64Encoded): boolean

      True, if content was sent as base64.
    - [body](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType/body): string

      Response body.
  + ### interface [Headers](https://bun.com/reference/node/inspector/Network/Headers)

    Request / response headers as keys / values of JSON object.
  + ### interface [Initiator](https://bun.com/reference/node/inspector/Network/Initiator)

    Information about the request initiator.

    - [columnNumber](https://bun.com/reference/node/inspector/Network/Initiator/columnNumber)?: number

      Initiator column number, set for Parser type or for Script type (when script is importing module) (0-based).
    - [lineNumber](https://bun.com/reference/node/inspector/Network/Initiator/lineNumber)?: number

      Initiator line number, set for Parser type or for Script type (when script is importing module) (0-based).
    - [requestId](https://bun.com/reference/node/inspector/Network/Initiator/requestId)?: string

      Set if another request triggered this request (e.g. preflight).
    - [stack](https://bun.com/reference/node/inspector/Network/Initiator/stack)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Initiator JavaScript stack trace, set for Script only. Requires the Debugger domain to be enabled.
    - [type](https://bun.com/reference/node/inspector/Network/Initiator/type): string

      Type of this initiator.
    - [url](https://bun.com/reference/node/inspector/Network/Initiator/url)?: string

      Initiator URL, set for Parser type or for Script type (when script is importing module) or for SignedExchange type.
  + ### interface [LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)

    - [errorText](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType/errorText): string

      Error message.
    - [requestId](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType/requestId): string

      Request identifier.
    - [timestamp](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType/timestamp): number

      Timestamp.
    - [type](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType/type): string

      Resource type.
  + ### interface [LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)

    - [requestId](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType/requestId): string

      Request identifier.
    - [timestamp](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType/timestamp): number

      Timestamp.
  + ### interface [LoadNetworkResourcePageResult](https://bun.com/reference/node/inspector/Network/LoadNetworkResourcePageResult)

    - [stream](https://bun.com/reference/node/inspector/Network/LoadNetworkResourcePageResult/stream)?: string
    - [success](https://bun.com/reference/node/inspector/Network/LoadNetworkResourcePageResult/success): boolean
  + ### interface [LoadNetworkResourceParameterType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceParameterType)

    - [url](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceParameterType/url): string

      URL of the resource to get content for.
  + ### interface [LoadNetworkResourceReturnType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceReturnType)

    - [resource](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceReturnType/resource): [LoadNetworkResourcePageResult](https://bun.com/reference/node/inspector/Network/LoadNetworkResourcePageResult)
  + ### interface [Request](https://bun.com/reference/node/inspector/Network/Request)

    HTTP request data.

    - [hasPostData](https://bun.com/reference/node/inspector/Network/Request/hasPostData): boolean
    - [headers](https://bun.com/reference/node/inspector/Network/Request/headers): [Headers](https://bun.com/reference/node/inspector/Network/Headers)
    - [method](https://bun.com/reference/node/inspector/Network/Request/method): string
    - [url](https://bun.com/reference/node/inspector/Network/Request/url): string
  + ### interface [RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)

    - [initiator](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType/initiator): [Initiator](https://bun.com/reference/node/inspector/Network/Initiator)

      Request initiator.
    - [request](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType/request): [Request](https://bun.com/reference/node/inspector/Network/Request)

      Request data.
    - [requestId](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType/requestId): string

      Request identifier.
    - [timestamp](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType/timestamp): number

      Timestamp.
    - [wallTime](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType/wallTime): number

      Timestamp.
  + ### interface [Response](https://bun.com/reference/node/inspector/Network/Response)

    HTTP response data.

    - [charset](https://bun.com/reference/node/inspector/Network/Response/charset): string
    - [headers](https://bun.com/reference/node/inspector/Network/Response/headers): [Headers](https://bun.com/reference/node/inspector/Network/Headers)
    - [mimeType](https://bun.com/reference/node/inspector/Network/Response/mimeType): string
    - [status](https://bun.com/reference/node/inspector/Network/Response/status): number
    - [statusText](https://bun.com/reference/node/inspector/Network/Response/statusText): string
    - [url](https://bun.com/reference/node/inspector/Network/Response/url): string
  + ### interface [ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)

    - [requestId](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType/requestId): string

      Request identifier.
    - [response](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType/response): [Response](https://bun.com/reference/node/inspector/Network/Response)

      Response data.
    - [timestamp](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType/timestamp): number

      Timestamp.
    - [type](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType/type): string

      Resource type.
  + ### interface [StreamResourceContentParameterType](https://bun.com/reference/node/inspector/Network/StreamResourceContentParameterType)

    - [requestId](https://bun.com/reference/node/inspector/Network/StreamResourceContentParameterType/requestId): string

      Identifier of the request to stream.
  + ### interface [StreamResourceContentReturnType](https://bun.com/reference/node/inspector/Network/StreamResourceContentReturnType)

    - [bufferedData](https://bun.com/reference/node/inspector/Network/StreamResourceContentReturnType/bufferedData): string

      Data that has been buffered until streaming is enabled.
  + ### interface [WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)

    - [requestId](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType/requestId): string

      Request identifier.
    - [timestamp](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType/timestamp): number

      Timestamp.
  + ### interface [WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)

    - [initiator](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType/initiator): [Initiator](https://bun.com/reference/node/inspector/Network/Initiator)

      Request initiator.
    - [requestId](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType/requestId): string

      Request identifier.
    - [url](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType/url): string

      WebSocket request URL.
  + ### interface [WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)

    - [requestId](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType/requestId): string

      Request identifier.
    - [response](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType/response): [WebSocketResponse](https://bun.com/reference/node/inspector/Network/WebSocketResponse)

      WebSocket response data.
    - [timestamp](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType/timestamp): number

      Timestamp.
  + ### interface [WebSocketResponse](https://bun.com/reference/node/inspector/Network/WebSocketResponse)

    WebSocket response data.

    - [headers](https://bun.com/reference/node/inspector/Network/WebSocketResponse/headers): [Headers](https://bun.com/reference/node/inspector/Network/Headers)

      HTTP response headers.
    - [status](https://bun.com/reference/node/inspector/Network/WebSocketResponse/status): number

      HTTP response status code.
    - [statusText](https://bun.com/reference/node/inspector/Network/WebSocketResponse/statusText): string

      HTTP response status text.
  + type [MonotonicTime](https://bun.com/reference/node/inspector/Network/MonotonicTime) = number

    Monotonically increasing time in seconds since an arbitrary point in the past.
  + type [RequestId](https://bun.com/reference/node/inspector/Network/RequestId) = string

    Unique request identifier.
  + type [ResourceType](https://bun.com/reference/node/inspector/Network/ResourceType) = string

    Resource type as it was perceived by the rendering engine.
  + type [TimeSinceEpoch](https://bun.com/reference/node/inspector/Network/TimeSinceEpoch) = number

    UTC time in seconds, counted from January 1, 1970.
  + function [dataReceived](https://bun.com/reference/node/inspector/Network/dataReceived)(

    params: [DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.dataReceived` event to connected frontends, or buffers the data if `Network.streamResourceContent` command was not invoked for the given request yet.

    Also enables `Network.getResponseBody` command to retrieve the response data.
  + function [dataSent](https://bun.com/reference/node/inspector/Network/dataSent)(

    params: unknown

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Enables `Network.getRequestPostData` command to retrieve the request data.
  + function [loadingFailed](https://bun.com/reference/node/inspector/Network/loadingFailed)(

    params: [LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.loadingFailed` event to connected frontends. This event indicates that HTTP request has failed to load.
  + function [loadingFinished](https://bun.com/reference/node/inspector/Network/loadingFinished)(

    params: [LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.loadingFinished` event to connected frontends. This event indicates that HTTP request has finished loading.
  + function [requestWillBeSent](https://bun.com/reference/node/inspector/Network/requestWillBeSent)(

    params: [RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.requestWillBeSent` event to connected frontends. This event indicates that the application is about to send an HTTP request.
  + function [responseReceived](https://bun.com/reference/node/inspector/Network/responseReceived)(

    params: [ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.responseReceived` event to connected frontends. This event indicates that HTTP response is available.
  + function [webSocketClosed](https://bun.com/reference/node/inspector/Network/webSocketClosed)(

    params: [WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.webSocketClosed` event to connected frontends. This event indicates that a WebSocket connection has been closed.
  + function [webSocketCreated](https://bun.com/reference/node/inspector/Network/webSocketCreated)(

    params: [WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.webSocketCreated` event to connected frontends. This event indicates that a WebSocket connection has been initiated.
  + function [webSocketHandshakeResponseReceived](https://bun.com/reference/node/inspector/Network/webSocketHandshakeResponseReceived)(

    params: [WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)

    ): void;

    This feature is only available with the `--experimental-network-inspection` flag enabled.

    Broadcasts the `Network.webSocketHandshakeResponseReceived` event to connected frontends. This event indicates that the WebSocket handshake response has been received.
* ### namespace [NetworkResources](https://bun.com/reference/node/inspector/NetworkResources)

  + function [put](https://bun.com/reference/node/inspector/NetworkResources/put)(

    url: string,

    data: string

    ): void;

    This feature is only available with the `--experimental-inspector-network-resource` flag enabled.

    The inspector.NetworkResources.put method is used to provide a response for a loadNetworkResource request issued via the Chrome DevTools Protocol (CDP). This is typically triggered when a source map is specified by URL, and a DevTools frontend—such as Chrome—requests the resource to retrieve the source map.

    This method allows developers to predefine the resource content to be served in response to such CDP requests.

    ```
    const inspector = require('node:inspector');
    // By preemptively calling put to register the resource, a source map can be resolved when
    // a loadNetworkResource request is made from the frontend.
    async function setNetworkResources() {
      const mapUrl = 'http://localhost:3000/dist/app.js.map';
      const tsUrl = 'http://localhost:3000/src/app.ts';
      const distAppJsMap = await fetch(mapUrl).then((res) => res.text());
      const srcAppTs = await fetch(tsUrl).then((res) => res.text());
      inspector.NetworkResources.put(mapUrl, distAppJsMap);
      inspector.NetworkResources.put(tsUrl, srcAppTs);
    };
    setNetworkResources().then(() => {
      require('./dist/app');
    });
    ```

    For more details, see the official CDP documentation: [Network.loadNetworkResource](https://chromedevtools.github.io/devtools-protocol/tot/Network/#method-loadNetworkResource)
* ### class [Session](https://bun.com/reference/node/inspector/Session)

  The `inspector.Session` is used for dispatching messages to the V8 inspector back-end and receiving message responses and notifications.

  + static [captureRejections](https://bun.com/reference/node/inspector/Session/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/inspector/Session/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/inspector/Session/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/inspector/Session/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/inspector/Session/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/Session/addListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [connect](https://bun.com/reference/node/inspector/Session/connect)(): void;

    Connects a session to the inspector back-end.
  + [connectToMainThread](https://bun.com/reference/node/inspector/Session/connectToMainThread)(): void;

    Connects a session to the inspector back-end. An exception will be thrown if this API was not called on a Worker thread.
  + [disconnect](https://bun.com/reference/node/inspector/Session/disconnect)(): void;

    Immediately close the session. All pending message callbacks will be called with an error. `session.connect()` will need to be called to be able to send messages again. Reconnected session will lose all inspector state, such as enabled agents or configured breakpoints.
  + [emit](https://bun.com/reference/node/inspector/Session/emit)(

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

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'inspectorNotification',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.executionContextCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.executionContextDestroyed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.executionContextsCleared'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.exceptionThrown',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.exceptionRevoked',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.consoleAPICalled',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Runtime.inspectRequested',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Debugger.scriptParsed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Debugger.scriptFailedToParse',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Debugger.breakpointResolved',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Debugger.paused',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Debugger.resumed'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Console.messageAdded',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Profiler.consoleProfileStarted',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Profiler.consoleProfileFinished',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'HeapProfiler.resetProfiles'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'HeapProfiler.lastSeenObjectId',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'HeapProfiler.heapStatsUpdate',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeTracing.dataCollected',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeTracing.tracingComplete'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeWorker.attachedToWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeWorker.detachedFromWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeWorker.receivedMessageFromWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.requestWillBeSent',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.responseReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.loadingFailed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.loadingFinished',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.dataReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.webSocketCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.webSocketClosed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Network.webSocketHandshakeResponseReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeRuntime.waitingForDisconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'NodeRuntime.waitingForDebugger'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Target.targetCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/Session/emit)(

    event: 'Target.attachedToTarget',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>

    ): boolean;
  + [eventNames](https://bun.com/reference/node/inspector/Session/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/inspector/Session/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/inspector/Session/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/inspector/Session/listeners)<K>(

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
  + [off](https://bun.com/reference/node/inspector/Session/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/inspector/Session/on)(

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

    @param event

    The name of the event.

    @param listener

    The callback function

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/Session/on)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [once](https://bun.com/reference/node/inspector/Session/once)(

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

    @param event

    The name of the event.

    @param listener

    The callback function

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/Session/once)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [post](https://bun.com/reference/node/inspector/Session/post)(

    method: string,

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params?: object) => void

    ): void;

    Posts a message to the inspector back-end. `callback` will be notified when a response is received. `callback` is a function that accepts two optional arguments: error and message-specific result.

    ```
    session.post('Runtime.evaluate', { expression: '2 + 2' },
                 (error, { result }) => console.log(result));
    // Output: { type: 'number', value: 4, description: '4' }
    ```

    The latest version of the V8 inspector protocol is published on the [Chrome DevTools Protocol Viewer](https://chromedevtools.github.io/devtools-protocol/v8/).

    Node.js inspector supports all the Chrome DevTools Protocol domains declared by V8. Chrome DevTools Protocol domain provides an interface for interacting with one of the runtime agents used to inspect the application state and listen to the run-time events.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: string,

    params?: object,

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params?: object) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Schema.getDomains',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetDomainsReturnType](https://bun.com/reference/node/inspector/Schema/GetDomainsReturnType)) => void

    ): void;

    Returns supported domains.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.evaluate',

    params?: [EvaluateParameterType](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [EvaluateReturnType](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType)) => void

    ): void;

    Evaluates expression on global object.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.evaluate',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [EvaluateReturnType](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.awaitPromise',

    params?: [AwaitPromiseParameterType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [AwaitPromiseReturnType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType)) => void

    ): void;

    Add handler to promise with given promise object id.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.awaitPromise',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [AwaitPromiseReturnType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.callFunctionOn',

    params?: [CallFunctionOnParameterType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [CallFunctionOnReturnType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType)) => void

    ): void;

    Calls function with given declaration on the given object. Object group of the result is inherited from the target object.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.callFunctionOn',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [CallFunctionOnReturnType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.getProperties',

    params?: [GetPropertiesParameterType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetPropertiesReturnType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType)) => void

    ): void;

    Returns properties of a given object. Object group of the result is inherited from the target object.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.getProperties',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetPropertiesReturnType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.releaseObject',

    params?: [ReleaseObjectParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Releases remote object with given id.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.releaseObject',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.releaseObjectGroup',

    params?: [ReleaseObjectGroupParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectGroupParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Releases all remote objects that belong to a given group.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.releaseObjectGroup',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.runIfWaitingForDebugger',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Tells inspected instance to run if it was waiting for debugger to attach.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enables reporting of execution contexts creation by means of <code>executionContextCreated</code> event. When the reporting gets enabled the event will be sent immediately for each existing execution context.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disables reporting of execution contexts creation.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.discardConsoleEntries',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Discards collected exceptions and console API calls.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.setCustomObjectFormatterEnabled',

    params?: [SetCustomObjectFormatterEnabledParameterType](https://bun.com/reference/node/inspector/Runtime/SetCustomObjectFormatterEnabledParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.setCustomObjectFormatterEnabled',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.compileScript',

    params?: [CompileScriptParameterType](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [CompileScriptReturnType](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType)) => void

    ): void;

    Compiles expression.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.compileScript',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [CompileScriptReturnType](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.runScript',

    params?: [RunScriptParameterType](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [RunScriptReturnType](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType)) => void

    ): void;

    Runs script with given id in a given context.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.runScript',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [RunScriptReturnType](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.queryObjects',

    params?: [QueryObjectsParameterType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [QueryObjectsReturnType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.queryObjects',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [QueryObjectsReturnType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.globalLexicalScopeNames',

    params?: [GlobalLexicalScopeNamesParameterType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GlobalLexicalScopeNamesReturnType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesReturnType)) => void

    ): void;

    Returns all let, const and class variables from global scope.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Runtime.globalLexicalScopeNames',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GlobalLexicalScopeNamesReturnType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [EnableReturnType](https://bun.com/reference/node/inspector/Debugger/EnableReturnType)) => void

    ): void;

    Enables debugger for the given page. Clients should not assume that the debugging has been enabled until the result for this command is received.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disables debugger for given page.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpointsActive',

    params?: [SetBreakpointsActiveParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointsActiveParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Activates / deactivates all breakpoints on the page.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpointsActive',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setSkipAllPauses',

    params?: [SetSkipAllPausesParameterType](https://bun.com/reference/node/inspector/Debugger/SetSkipAllPausesParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Makes page not interrupt on any pauses (breakpoint, exception, dom exception etc).

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setSkipAllPauses',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpointByUrl',

    params?: [SetBreakpointByUrlParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetBreakpointByUrlReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType)) => void

    ): void;

    Sets JavaScript breakpoint at given location specified either by URL or URL regex. Once this command is issued, all existing parsed scripts will have breakpoints resolved and returned in <code>locations</code> property. Further matching script parsing will result in subsequent <code>breakpointResolved</code> events issued. This logical breakpoint will survive page reloads.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpointByUrl',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetBreakpointByUrlReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpoint',

    params?: [SetBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetBreakpointReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType)) => void

    ): void;

    Sets JavaScript breakpoint at a given location.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBreakpoint',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetBreakpointReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.removeBreakpoint',

    params?: [RemoveBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/RemoveBreakpointParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Removes JavaScript breakpoint.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.removeBreakpoint',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getPossibleBreakpoints',

    params?: [GetPossibleBreakpointsParameterType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetPossibleBreakpointsReturnType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsReturnType)) => void

    ): void;

    Returns possible locations for breakpoint. scriptId in start and end range locations should be the same.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getPossibleBreakpoints',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetPossibleBreakpointsReturnType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.continueToLocation',

    params?: [ContinueToLocationParameterType](https://bun.com/reference/node/inspector/Debugger/ContinueToLocationParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Continues execution until specific location is reached.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.continueToLocation',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.pauseOnAsyncCall',

    params?: [PauseOnAsyncCallParameterType](https://bun.com/reference/node/inspector/Debugger/PauseOnAsyncCallParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.pauseOnAsyncCall',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.stepOver',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Steps over the statement.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.stepInto',

    params?: [StepIntoParameterType](https://bun.com/reference/node/inspector/Debugger/StepIntoParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Steps into the function call.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.stepInto',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.stepOut',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Steps out of the function call.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.pause',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Stops on the next JavaScript statement.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.resume',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Resumes JavaScript execution.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getStackTrace',

    params?: [GetStackTraceParameterType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetStackTraceReturnType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceReturnType)) => void

    ): void;

    Returns stack trace with given <code>stackTraceId</code>.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getStackTrace',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetStackTraceReturnType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.searchInContent',

    params?: [SearchInContentParameterType](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SearchInContentReturnType](https://bun.com/reference/node/inspector/Debugger/SearchInContentReturnType)) => void

    ): void;

    Searches for given string in script content.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.searchInContent',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SearchInContentReturnType](https://bun.com/reference/node/inspector/Debugger/SearchInContentReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setScriptSource',

    params?: [SetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType)) => void

    ): void;

    Edits JavaScript source live.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setScriptSource',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [SetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.restartFrame',

    params?: [RestartFrameParameterType](https://bun.com/reference/node/inspector/Debugger/RestartFrameParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [RestartFrameReturnType](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType)) => void

    ): void;

    Restarts particular call frame from the beginning.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.restartFrame',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [RestartFrameReturnType](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getScriptSource',

    params?: [GetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceReturnType)) => void

    ): void;

    Returns source for the script with given id.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.getScriptSource',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setPauseOnExceptions',

    params?: [SetPauseOnExceptionsParameterType](https://bun.com/reference/node/inspector/Debugger/SetPauseOnExceptionsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Defines pause on exceptions state. Can be set to stop on all exceptions, uncaught exceptions or no exceptions. Initial pause on exceptions state is <code>none</code>.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setPauseOnExceptions',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.evaluateOnCallFrame',

    params?: [EvaluateOnCallFrameParameterType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [EvaluateOnCallFrameReturnType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType)) => void

    ): void;

    Evaluates expression on a given call frame.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.evaluateOnCallFrame',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [EvaluateOnCallFrameReturnType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setVariableValue',

    params?: [SetVariableValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Changes value of variable in a callframe. Object-based scopes are not supported and must be mutated manually.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setVariableValue',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setReturnValue',

    params?: [SetReturnValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetReturnValueParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Changes return value in top frame. Available only at return break position.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setReturnValue',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setAsyncCallStackDepth',

    params?: [SetAsyncCallStackDepthParameterType](https://bun.com/reference/node/inspector/Debugger/SetAsyncCallStackDepthParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enables or disables async call stacks tracking.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setAsyncCallStackDepth',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBlackboxPatterns',

    params?: [SetBlackboxPatternsParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxPatternsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Replace previous blackbox patterns with passed ones. Forces backend to skip stepping/pausing in scripts with url matching one of the patterns. VM will try to leave blackboxed script by performing 'step in' several times, finally resorting to 'step out' if unsuccessful.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBlackboxPatterns',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBlackboxedRanges',

    params?: [SetBlackboxedRangesParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxedRangesParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Makes backend skip steps in the script in blackboxed ranges. VM will try leave blacklisted scripts by performing 'step in' several times, finally resorting to 'step out' if unsuccessful. Positions array contains positions where blackbox state is changed. First interval isn't blackboxed. Array should be sorted.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Debugger.setBlackboxedRanges',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Console.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enables console domain, sends the messages collected so far to the client by means of the <code>messageAdded</code> notification.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Console.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disables console domain, prevents further console messages from being reported to the client.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Console.clearMessages',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Does nothing.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.setSamplingInterval',

    params?: [SetSamplingIntervalParameterType](https://bun.com/reference/node/inspector/Profiler/SetSamplingIntervalParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Changes CPU profiler sampling interval. Must be called before CPU profiles recording started.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.setSamplingInterval',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.start',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.stop',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [StopReturnType](https://bun.com/reference/node/inspector/Profiler/StopReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.startPreciseCoverage',

    params?: [StartPreciseCoverageParameterType](https://bun.com/reference/node/inspector/Profiler/StartPreciseCoverageParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enable precise code coverage. Coverage data for JavaScript executed before enabling precise code coverage may be incomplete. Enabling prevents running optimized code and resets execution counters.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.startPreciseCoverage',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.stopPreciseCoverage',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disable precise code coverage. Disabling releases unnecessary execution count records and allows executing optimized code.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.takePreciseCoverage',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [TakePreciseCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/TakePreciseCoverageReturnType)) => void

    ): void;

    Collect coverage data for the current isolate, and resets execution counters. Precise code coverage needs to have started.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Profiler.getBestEffortCoverage',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetBestEffortCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/GetBestEffortCoverageReturnType)) => void

    ): void;

    Collect coverage data for the current isolate. The coverage data may be incomplete due to garbage collection.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.startTrackingHeapObjects',

    params?: [StartTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartTrackingHeapObjectsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.startTrackingHeapObjects',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.stopTrackingHeapObjects',

    params?: [StopTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StopTrackingHeapObjectsParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.stopTrackingHeapObjects',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.takeHeapSnapshot',

    params?: [TakeHeapSnapshotParameterType](https://bun.com/reference/node/inspector/HeapProfiler/TakeHeapSnapshotParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.takeHeapSnapshot',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.collectGarbage',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.getObjectByHeapObjectId',

    params?: [GetObjectByHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetObjectByHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.getObjectByHeapObjectId',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetObjectByHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.addInspectedHeapObject',

    params?: [AddInspectedHeapObjectParameterType](https://bun.com/reference/node/inspector/HeapProfiler/AddInspectedHeapObjectParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enables console to refer to the node with given id via $x (see Command Line API for more details $x functions).

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.addInspectedHeapObject',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.getHeapObjectId',

    params?: [GetHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.getHeapObjectId',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.startSampling',

    params?: [StartSamplingParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartSamplingParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.startSampling',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.stopSampling',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [StopSamplingReturnType](https://bun.com/reference/node/inspector/HeapProfiler/StopSamplingReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'HeapProfiler.getSamplingProfile',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetSamplingProfileReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetSamplingProfileReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeTracing.getCategories',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetCategoriesReturnType](https://bun.com/reference/node/inspector/NodeTracing/GetCategoriesReturnType)) => void

    ): void;

    Gets supported tracing categories.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeTracing.start',

    params?: [StartParameterType](https://bun.com/reference/node/inspector/NodeTracing/StartParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Start trace events collection.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeTracing.start',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeTracing.stop',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Stop trace events collection. Remaining collected events will be sent as a sequence of dataCollected events followed by tracingComplete event.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.sendMessageToWorker',

    params?: [SendMessageToWorkerParameterType](https://bun.com/reference/node/inspector/NodeWorker/SendMessageToWorkerParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Sends protocol message over session with given id.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.sendMessageToWorker',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.enable',

    params?: [EnableParameterType](https://bun.com/reference/node/inspector/NodeWorker/EnableParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Instructs the inspector to attach to running workers. Will also attach to new workers as they start

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Detaches from all running workers and disables attaching to new workers as they are started.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.detach',

    params?: [DetachParameterType](https://bun.com/reference/node/inspector/NodeWorker/DetachParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Detached from the worker with given sessionId.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeWorker.detach',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disables network tracking, prevents network events from being sent to the client.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enables network tracking, network events will now be delivered to the client.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.getRequestPostData',

    params?: [GetRequestPostDataParameterType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetRequestPostDataReturnType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataReturnType)) => void

    ): void;

    Returns post data sent with the request. Returns an error when no data was sent with the request.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.getRequestPostData',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetRequestPostDataReturnType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.getResponseBody',

    params?: [GetResponseBodyParameterType](https://bun.com/reference/node/inspector/Network/GetResponseBodyParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetResponseBodyReturnType](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType)) => void

    ): void;

    Returns content served for the given request.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.getResponseBody',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [GetResponseBodyReturnType](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.streamResourceContent',

    params?: [StreamResourceContentParameterType](https://bun.com/reference/node/inspector/Network/StreamResourceContentParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [StreamResourceContentReturnType](https://bun.com/reference/node/inspector/Network/StreamResourceContentReturnType)) => void

    ): void;

    Enables streaming of the response for the given requestId. If enabled, the dataReceived event contains the data that was received during streaming.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.streamResourceContent',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [StreamResourceContentReturnType](https://bun.com/reference/node/inspector/Network/StreamResourceContentReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.loadNetworkResource',

    params?: [LoadNetworkResourceParameterType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [LoadNetworkResourceReturnType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceReturnType)) => void

    ): void;

    Fetches the resource and returns the content.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Network.loadNetworkResource',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [LoadNetworkResourceReturnType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeRuntime.enable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enable the NodeRuntime events except by `NodeRuntime.waitingForDisconnect`.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeRuntime.disable',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Disable NodeRuntime events

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeRuntime.notifyWhenWaitingForDisconnect',

    params?: [NotifyWhenWaitingForDisconnectParameterType](https://bun.com/reference/node/inspector/NodeRuntime/NotifyWhenWaitingForDisconnectParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Enable the `NodeRuntime.waitingForDisconnect`.

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'NodeRuntime.notifyWhenWaitingForDisconnect',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Target.setAutoAttach',

    params?: [SetAutoAttachParameterType](https://bun.com/reference/node/inspector/Target/SetAutoAttachParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'Target.setAutoAttach',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'IO.read',

    params?: [ReadParameterType](https://bun.com/reference/node/inspector/IO/ReadParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [ReadReturnType](https://bun.com/reference/node/inspector/IO/ReadReturnType)) => void

    ): void;

    Read a chunk of the stream

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'IO.read',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), params: [ReadReturnType](https://bun.com/reference/node/inspector/IO/ReadReturnType)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'IO.close',

    params?: [CloseParameterType](https://bun.com/reference/node/inspector/IO/CloseParameterType),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    [post](https://bun.com/reference/node/inspector/Session/post)(

    method: 'IO.close',

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

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

    @param event

    The name of the event.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/Session/prependListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

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

    @param event

    The name of the event.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/Session/prependOnceListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/inspector/Session/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/inspector/Session/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/inspector/Session/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/inspector/Session/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/inspector/Session/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/inspector/Session/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/inspector/Session/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/inspector/Session/on)(

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

    static [on](https://bun.com/reference/node/inspector/Session/on)(

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
  + static [once](https://bun.com/reference/node/inspector/Session/once)(

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

    static [once](https://bun.com/reference/node/inspector/Session/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/inspector/Session/setMaxListeners)(

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
* const [console](https://bun.com/reference/node/inspector/console): [InspectorConsole](https://bun.com/reference/node/inspector/InspectorConsole)

  An object to send messages to the remote inspector console.
* function [close](https://bun.com/reference/node/inspector/close)(): void;

  Deactivate the inspector. Blocks until there are no active connections.
* function [open](https://bun.com/reference/node/inspector/open)(

  port?: number,

  host?: string,

  wait?: boolean

  ): Disposable;

  Activate inspector on host and port. Equivalent to `node --inspect=[[host:]port]`, but can be done programmatically after node has started.

  If wait is `true`, will block until a client has connected to the inspect port and flow control has been passed to the debugger client.

  See the [security warning](https://nodejs.org/docs/latest-v24.x/api/cli.html#warning-binding-inspector-to-a-public-ipport-combination-is-insecure) regarding the `host` parameter usage.

  @param port

  Port to listen on for inspector connections. Defaults to what was specified on the CLI.

  @param host

  Host to listen on for inspector connections. Defaults to what was specified on the CLI.

  @param wait

  Block until a client has connected. Defaults to what was specified on the CLI.

  @returns

  Disposable that calls `inspector.close()`.
* function [url](https://bun.com/reference/node/inspector/url)(): undefined | string;

  Return the URL of the active inspector, or `undefined` if there is none.

  ```
  $ node --inspect -p 'inspector.url()'
  Debugger listening on ws://127.0.0.1:9229/166e272e-7a30-4d09-97ce-f1c012b43c34
  For help, see: https://nodejs.org/en/docs/inspector
  ws://127.0.0.1:9229/166e272e-7a30-4d09-97ce-f1c012b43c34

  $ node --inspect=localhost:3000 -p 'inspector.url()'
  Debugger listening on ws://localhost:3000/51cf8d0e-3c36-4c59-8efd-54519839e56a
  For help, see: https://nodejs.org/en/docs/inspector
  ws://localhost:3000/51cf8d0e-3c36-4c59-8efd-54519839e56a

  $ node -p 'inspector.url()'
  undefined
  ```
* function [waitForDebugger](https://bun.com/reference/node/inspector/waitForDebugger)(): void;

  Blocks until a client (existing or connected later) has sent `Runtime.runIfWaitingForDebugger` command.

  An exception will be thrown if there is no active inspector.

## Type definitions

* ### namespace [Console](https://bun.com/reference/node/inspector/Console)

  + ### interface [ConsoleMessage](https://bun.com/reference/node/inspector/Console/ConsoleMessage)

    Console message.

    - [column](https://bun.com/reference/node/inspector/Console/ConsoleMessage/column)?: number

      Column number in the resource that generated this message (1-based).
    - [level](https://bun.com/reference/node/inspector/Console/ConsoleMessage/level): string

      Message severity.
    - [line](https://bun.com/reference/node/inspector/Console/ConsoleMessage/line)?: number

      Line number in the resource that generated this message (1-based).
    - [source](https://bun.com/reference/node/inspector/Console/ConsoleMessage/source): string

      Message source.
    - [text](https://bun.com/reference/node/inspector/Console/ConsoleMessage/text): string

      Message text.
    - [url](https://bun.com/reference/node/inspector/Console/ConsoleMessage/url)?: string

      URL of the message origin.
  + ### interface [MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)

    - [message](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType/message): [ConsoleMessage](https://bun.com/reference/node/inspector/Console/ConsoleMessage)

      Console message that has been added.
* ### namespace [Debugger](https://bun.com/reference/node/inspector/Debugger)

  + ### interface [BreakLocation](https://bun.com/reference/node/inspector/Debugger/BreakLocation)

    - [columnNumber](https://bun.com/reference/node/inspector/Debugger/BreakLocation/columnNumber)?: number

      Column number in the script (0-based).
    - [lineNumber](https://bun.com/reference/node/inspector/Debugger/BreakLocation/lineNumber): number

      Line number in the script (0-based).
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/BreakLocation/scriptId): string

      Script identifier as reported in the <code>Debugger.scriptParsed</code>.
    - [type](https://bun.com/reference/node/inspector/Debugger/BreakLocation/type)?: string
  + ### interface [BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)

    - [breakpointId](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType/breakpointId): string

      Breakpoint unique identifier.
    - [location](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Actual breakpoint location.
  + ### interface [CallFrame](https://bun.com/reference/node/inspector/Debugger/CallFrame)

    JavaScript call frame. Array of call frames form the call stack.

    - [callFrameId](https://bun.com/reference/node/inspector/Debugger/CallFrame/callFrameId): string

      Call frame identifier. This identifier is only valid while the virtual machine is paused.
    - [functionLocation](https://bun.com/reference/node/inspector/Debugger/CallFrame/functionLocation)?: [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location in the source code.
    - [functionName](https://bun.com/reference/node/inspector/Debugger/CallFrame/functionName): string

      Name of the JavaScript function called on this call frame.
    - [location](https://bun.com/reference/node/inspector/Debugger/CallFrame/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location in the source code.
    - [returnValue](https://bun.com/reference/node/inspector/Debugger/CallFrame/returnValue)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      The value being returned, if the function is at return point.
    - [scopeChain](https://bun.com/reference/node/inspector/Debugger/CallFrame/scopeChain): [Scope](https://bun.com/reference/node/inspector/Debugger/Scope)[]

      Scope chain for this call frame.
    - [this](https://bun.com/reference/node/inspector/Debugger/CallFrame/this): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      <code>this</code> object for this call frame.
    - [url](https://bun.com/reference/node/inspector/Debugger/CallFrame/url): string

      JavaScript script name or url.
  + ### interface [ContinueToLocationParameterType](https://bun.com/reference/node/inspector/Debugger/ContinueToLocationParameterType)

    - [location](https://bun.com/reference/node/inspector/Debugger/ContinueToLocationParameterType/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location to continue to.
    - [targetCallFrames](https://bun.com/reference/node/inspector/Debugger/ContinueToLocationParameterType/targetCallFrames)?: string
  + ### interface [EnableReturnType](https://bun.com/reference/node/inspector/Debugger/EnableReturnType)

    - [debuggerId](https://bun.com/reference/node/inspector/Debugger/EnableReturnType/debuggerId): string

      Unique identifier of the debugger.
  + ### interface [EvaluateOnCallFrameParameterType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType)

    - [callFrameId](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/callFrameId): string

      Call frame identifier to evaluate on.
    - [expression](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/expression): string

      Expression to evaluate.
    - [generatePreview](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/generatePreview)?: boolean

      Whether preview should be generated for the result.
    - [includeCommandLineAPI](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/includeCommandLineAPI)?: boolean

      Specifies whether command line API should be available to the evaluated expression, defaults to false.
    - [objectGroup](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/objectGroup)?: string

      String object group name to put result into (allows rapid releasing resulting object handles using <code>releaseObjectGroup</code>).
    - [returnByValue](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/returnByValue)?: boolean

      Whether the result is expected to be a JSON object that should be sent by value.
    - [silent](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/silent)?: boolean

      In silent mode exceptions thrown during evaluation are not reported and do not pause execution. Overrides <code>setPauseOnException</code> state.
    - [throwOnSideEffect](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType/throwOnSideEffect)?: boolean

      Whether to throw an exception if side effect cannot be ruled out during evaluation.
  + ### interface [EvaluateOnCallFrameReturnType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [result](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Object wrapper for the evaluation result.
  + ### interface [GetPossibleBreakpointsParameterType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType)

    - [end](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType/end)?: [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      End of range to search possible breakpoint locations in (excluding). When not specified, end of scripts is used as end of range.
    - [restrictToFunction](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType/restrictToFunction)?: boolean

      Only consider locations which are in the same (non-nested) function as start.
    - [start](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType/start): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Start of range to search possible breakpoint locations in.
  + ### interface [GetPossibleBreakpointsReturnType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsReturnType)

    - [locations](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsReturnType/locations): [BreakLocation](https://bun.com/reference/node/inspector/Debugger/BreakLocation)[]

      List of the possible breakpoint locations.
  + ### interface [GetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceParameterType)

    - [scriptId](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceParameterType/scriptId): string

      Id of the script to get source for.
  + ### interface [GetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceReturnType)

    - [scriptSource](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceReturnType/scriptSource): string

      Script source.
  + ### interface [GetStackTraceParameterType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceParameterType)

    - [stackTraceId](https://bun.com/reference/node/inspector/Debugger/GetStackTraceParameterType/stackTraceId): [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)
  + ### interface [GetStackTraceReturnType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceReturnType)

    - [stackTrace](https://bun.com/reference/node/inspector/Debugger/GetStackTraceReturnType/stackTrace): [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)
  + ### interface [Location](https://bun.com/reference/node/inspector/Debugger/Location)

    Location in the source code.

    - [columnNumber](https://bun.com/reference/node/inspector/Debugger/Location/columnNumber)?: number

      Column number in the script (0-based).
    - [lineNumber](https://bun.com/reference/node/inspector/Debugger/Location/lineNumber): number

      Line number in the script (0-based).
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/Location/scriptId): string

      Script identifier as reported in the <code>Debugger.scriptParsed</code>.
  + ### interface [PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)

    - [asyncCallStackTraceId](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/asyncCallStackTraceId)?: [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Just scheduled async call will have this stack trace as parent stack during async execution. This field is available only after <code>Debugger.stepInto</code> call with <code>breakOnAsynCall</code> flag.
    - [asyncStackTrace](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/asyncStackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Async stack trace, if any.
    - [asyncStackTraceId](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/asyncStackTraceId)?: [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Async stack trace, if any.
    - [callFrames](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/callFrames): [CallFrame](https://bun.com/reference/node/inspector/Debugger/CallFrame)[]

      Call stack the virtual machine stopped on.
    - [data](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/data)?: object

      Object containing break-specific auxiliary properties.
    - [hitBreakpoints](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/hitBreakpoints)?: string[]

      Hit breakpoints IDs
    - [reason](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType/reason): string

      Pause reason.
  + ### interface [PauseOnAsyncCallParameterType](https://bun.com/reference/node/inspector/Debugger/PauseOnAsyncCallParameterType)

    - [parentStackTraceId](https://bun.com/reference/node/inspector/Debugger/PauseOnAsyncCallParameterType/parentStackTraceId): [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Debugger will pause when async call with given stack trace is started.
  + ### interface [RemoveBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/RemoveBreakpointParameterType)

    - [breakpointId](https://bun.com/reference/node/inspector/Debugger/RemoveBreakpointParameterType/breakpointId): string
  + ### interface [RestartFrameParameterType](https://bun.com/reference/node/inspector/Debugger/RestartFrameParameterType)

    - [callFrameId](https://bun.com/reference/node/inspector/Debugger/RestartFrameParameterType/callFrameId): string

      Call frame identifier to evaluate on.
  + ### interface [RestartFrameReturnType](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType)

    - [asyncStackTrace](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType/asyncStackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Async stack trace, if any.
    - [asyncStackTraceId](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType/asyncStackTraceId)?: [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Async stack trace, if any.
    - [callFrames](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType/callFrames): [CallFrame](https://bun.com/reference/node/inspector/Debugger/CallFrame)[]

      New stack trace.
  + ### interface [Scope](https://bun.com/reference/node/inspector/Debugger/Scope)

    Scope description.

    - [endLocation](https://bun.com/reference/node/inspector/Debugger/Scope/endLocation)?: [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location in the source code where scope ends
    - [name](https://bun.com/reference/node/inspector/Debugger/Scope/name)?: string
    - [object](https://bun.com/reference/node/inspector/Debugger/Scope/object): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Object representing the scope. For <code>global</code> and <code>with</code> scopes it represents the actual object; for the rest of the scopes, it is artificial transient object enumerating scope variables as its properties.
    - [startLocation](https://bun.com/reference/node/inspector/Debugger/Scope/startLocation)?: [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location in the source code where scope starts
    - [type](https://bun.com/reference/node/inspector/Debugger/Scope/type): string

      Scope type.
  + ### interface [ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)

    - [endColumn](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/endColumn): number

      Length of the last line of the script.
    - [endLine](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/endLine): number

      Last line of the script.
    - [executionContextAuxData](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/executionContextAuxData)?: object

      Embedder-specific auxiliary data.
    - [executionContextId](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/executionContextId): number

      Specifies script creation context.
    - [hash](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/hash): string

      Content hash of the script.
    - [hasSourceURL](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/hasSourceURL)?: boolean

      True, if this script has sourceURL.
    - [isModule](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/isModule)?: boolean

      True, if this script is ES6 module.
    - [length](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/length)?: number

      This script length.
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/scriptId): string

      Identifier of the script parsed.
    - [sourceMapURL](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/sourceMapURL)?: string

      URL of source map associated with script (if any).
    - [stackTrace](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/stackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      JavaScript top stack frame of where the script parsed event was triggered if available.
    - [startColumn](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/startColumn): number

      Column offset of the script within the resource with given URL.
    - [startLine](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/startLine): number

      Line offset of the script within the resource with given URL (for script tags).
    - [url](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType/url): string

      URL or name of the script parsed (if any).
  + ### interface [ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)

    - [endColumn](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/endColumn): number

      Length of the last line of the script.
    - [endLine](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/endLine): number

      Last line of the script.
    - [executionContextAuxData](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/executionContextAuxData)?: object

      Embedder-specific auxiliary data.
    - [executionContextId](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/executionContextId): number

      Specifies script creation context.
    - [hash](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/hash): string

      Content hash of the script.
    - [hasSourceURL](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/hasSourceURL)?: boolean

      True, if this script has sourceURL.
    - [isLiveEdit](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/isLiveEdit)?: boolean

      True, if this script is generated as a result of the live edit operation.
    - [isModule](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/isModule)?: boolean

      True, if this script is ES6 module.
    - [length](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/length)?: number

      This script length.
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/scriptId): string

      Identifier of the script parsed.
    - [sourceMapURL](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/sourceMapURL)?: string

      URL of source map associated with script (if any).
    - [stackTrace](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/stackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      JavaScript top stack frame of where the script parsed event was triggered if available.
    - [startColumn](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/startColumn): number

      Column offset of the script within the resource with given URL.
    - [startLine](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/startLine): number

      Line offset of the script within the resource with given URL (for script tags).
    - [url](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType/url): string

      URL or name of the script parsed (if any).
  + ### interface [ScriptPosition](https://bun.com/reference/node/inspector/Debugger/ScriptPosition)

    Location in the source code.

    - [columnNumber](https://bun.com/reference/node/inspector/Debugger/ScriptPosition/columnNumber): number
    - [lineNumber](https://bun.com/reference/node/inspector/Debugger/ScriptPosition/lineNumber): number
  + ### interface [SearchInContentParameterType](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType)

    - [caseSensitive](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType/caseSensitive)?: boolean

      If true, search is case sensitive.
    - [isRegex](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType/isRegex)?: boolean

      If true, treats string parameter as regex.
    - [query](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType/query): string

      String to search for.
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType/scriptId): string

      Id of the script to search in.
  + ### interface [SearchInContentReturnType](https://bun.com/reference/node/inspector/Debugger/SearchInContentReturnType)

    - [result](https://bun.com/reference/node/inspector/Debugger/SearchInContentReturnType/result): [SearchMatch](https://bun.com/reference/node/inspector/Debugger/SearchMatch)[]

      List of search matches.
  + ### interface [SearchMatch](https://bun.com/reference/node/inspector/Debugger/SearchMatch)

    Search match for resource.

    - [lineContent](https://bun.com/reference/node/inspector/Debugger/SearchMatch/lineContent): string

      Line with match content.
    - [lineNumber](https://bun.com/reference/node/inspector/Debugger/SearchMatch/lineNumber): number

      Line number in resource content.
  + ### interface [SetAsyncCallStackDepthParameterType](https://bun.com/reference/node/inspector/Debugger/SetAsyncCallStackDepthParameterType)

    - [maxDepth](https://bun.com/reference/node/inspector/Debugger/SetAsyncCallStackDepthParameterType/maxDepth): number

      Maximum depth of async call stacks. Setting to <code>0</code> will effectively disable collecting async call stacks (default).
  + ### interface [SetBlackboxedRangesParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxedRangesParameterType)

    - [positions](https://bun.com/reference/node/inspector/Debugger/SetBlackboxedRangesParameterType/positions): [ScriptPosition](https://bun.com/reference/node/inspector/Debugger/ScriptPosition)[]
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/SetBlackboxedRangesParameterType/scriptId): string

      Id of the script.
  + ### interface [SetBlackboxPatternsParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxPatternsParameterType)

    - [patterns](https://bun.com/reference/node/inspector/Debugger/SetBlackboxPatternsParameterType/patterns): string[]

      Array of regexps that will be used to check script url for blackbox state.
  + ### interface [SetBreakpointByUrlParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType)

    - [columnNumber](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/columnNumber)?: number

      Offset in the line to set breakpoint at.
    - [condition](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/condition)?: string

      Expression to use as a breakpoint condition. When specified, debugger will only stop on the breakpoint if this expression evaluates to true.
    - [lineNumber](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/lineNumber): number

      Line number to set breakpoint at.
    - [scriptHash](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/scriptHash)?: string

      Script hash of the resources to set breakpoint on.
    - [url](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/url)?: string

      URL of the resources to set breakpoint on.
    - [urlRegex](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType/urlRegex)?: string

      Regex pattern for the URLs of the resources to set breakpoints on. Either <code>url</code> or <code>urlRegex</code> must be specified.
  + ### interface [SetBreakpointByUrlReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType)

    - [breakpointId](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType/breakpointId): string

      Id of the created breakpoint for further reference.
    - [locations](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType/locations): [Location](https://bun.com/reference/node/inspector/Debugger/Location)[]

      List of the locations this breakpoint resolved into upon addition.
  + ### interface [SetBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointParameterType)

    - [condition](https://bun.com/reference/node/inspector/Debugger/SetBreakpointParameterType/condition)?: string

      Expression to use as a breakpoint condition. When specified, debugger will only stop on the breakpoint if this expression evaluates to true.
    - [location](https://bun.com/reference/node/inspector/Debugger/SetBreakpointParameterType/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location to set breakpoint in.
  + ### interface [SetBreakpointReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType)

    - [actualLocation](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType/actualLocation): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location this breakpoint resolved into.
    - [breakpointId](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType/breakpointId): string

      Id of the created breakpoint for further reference.
  + ### interface [SetBreakpointsActiveParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointsActiveParameterType)

    - [active](https://bun.com/reference/node/inspector/Debugger/SetBreakpointsActiveParameterType/active): boolean

      New value for breakpoints active state.
  + ### interface [SetPauseOnExceptionsParameterType](https://bun.com/reference/node/inspector/Debugger/SetPauseOnExceptionsParameterType)

    - [state](https://bun.com/reference/node/inspector/Debugger/SetPauseOnExceptionsParameterType/state): string

      Pause on exceptions mode.
  + ### interface [SetReturnValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetReturnValueParameterType)

    - [newValue](https://bun.com/reference/node/inspector/Debugger/SetReturnValueParameterType/newValue): [CallArgument](https://bun.com/reference/node/inspector/Runtime/CallArgument)

      New return value.
  + ### interface [SetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType)

    - [dryRun](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType/dryRun)?: boolean

      If true the change will not actually be applied. Dry run may be used to get result description without actually modifying the code.
    - [scriptId](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType/scriptId): string

      Id of the script to edit.
    - [scriptSource](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType/scriptSource): string

      New content of the script.
  + ### interface [SetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType)

    - [asyncStackTrace](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType/asyncStackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Async stack trace, if any.
    - [asyncStackTraceId](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType/asyncStackTraceId)?: [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Async stack trace, if any.
    - [callFrames](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType/callFrames)?: [CallFrame](https://bun.com/reference/node/inspector/Debugger/CallFrame)[]

      New stack trace in case editing has happened while VM was stopped.
    - [exceptionDetails](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details if any.
    - [stackChanged](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType/stackChanged)?: boolean

      Whether current call stack was modified after applying the changes.
  + ### interface [SetSkipAllPausesParameterType](https://bun.com/reference/node/inspector/Debugger/SetSkipAllPausesParameterType)

    - [skip](https://bun.com/reference/node/inspector/Debugger/SetSkipAllPausesParameterType/skip): boolean

      New value for skip pauses state.
  + ### interface [SetVariableValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType)

    - [callFrameId](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType/callFrameId): string

      Id of callframe that holds variable.
    - [newValue](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType/newValue): [CallArgument](https://bun.com/reference/node/inspector/Runtime/CallArgument)

      New variable value.
    - [scopeNumber](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType/scopeNumber): number

      0-based number of scope as was listed in scope chain. Only 'local', 'closure' and 'catch' scope types are allowed. Other scopes could be manipulated manually.
    - [variableName](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType/variableName): string

      Variable name.
  + ### interface [StepIntoParameterType](https://bun.com/reference/node/inspector/Debugger/StepIntoParameterType)

    - [breakOnAsyncCall](https://bun.com/reference/node/inspector/Debugger/StepIntoParameterType/breakOnAsyncCall)?: boolean

      Debugger will issue additional Debugger.paused notification if any async task is scheduled before next pause.
  + type [BreakpointId](https://bun.com/reference/node/inspector/Debugger/BreakpointId) = string

    Breakpoint identifier.
  + type [CallFrameId](https://bun.com/reference/node/inspector/Debugger/CallFrameId) = string

    Call frame identifier.
* ### namespace [HeapProfiler](https://bun.com/reference/node/inspector/HeapProfiler)

  + ### interface [AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)

    - [chunk](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType/chunk): string
  + ### interface [AddInspectedHeapObjectParameterType](https://bun.com/reference/node/inspector/HeapProfiler/AddInspectedHeapObjectParameterType)

    - [heapObjectId](https://bun.com/reference/node/inspector/HeapProfiler/AddInspectedHeapObjectParameterType/heapObjectId): string

      Heap snapshot object id to be accessible by means of $x command line API.
  + ### interface [GetHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdParameterType)

    - [objectId](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdParameterType/objectId): string

      Identifier of the object to get heap object id for.
  + ### interface [GetHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdReturnType)

    - [heapSnapshotObjectId](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdReturnType/heapSnapshotObjectId): string

      Id of the heap snapshot object corresponding to the passed remote object id.
  + ### interface [GetObjectByHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdParameterType)

    - [objectGroup](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdParameterType/objectGroup)?: string

      Symbolic group name that can be used to release multiple objects.
    - [objectId](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdParameterType/objectId): string
  + ### interface [GetObjectByHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdReturnType)

    - [result](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Evaluation result.
  + ### interface [GetSamplingProfileReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetSamplingProfileReturnType)

    - [profile](https://bun.com/reference/node/inspector/HeapProfiler/GetSamplingProfileReturnType/profile): [SamplingHeapProfile](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfile)

      Return the sampling profile being collected.
  + ### interface [HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)

    - [statsUpdate](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType/statsUpdate): number[]

      An array of triplets. Each triplet describes a fragment. The first integer is the fragment index, the second integer is a total count of objects for the fragment, the third integer is a total size of the objects for the fragment.
  + ### interface [LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)

    - [lastSeenObjectId](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType/lastSeenObjectId): number
    - [timestamp](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType/timestamp): number
  + ### interface [ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)

    - [done](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType/done): number
    - [finished](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType/finished)?: boolean
    - [total](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType/total): number
  + ### interface [SamplingHeapProfile](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfile)

    Profile.

    - [head](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfile/head): [SamplingHeapProfileNode](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode)
  + ### interface [SamplingHeapProfileNode](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode)

    Sampling Heap Profile node. Holds callsite information, allocation statistics and child nodes.

    - [callFrame](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode/callFrame): [CallFrame](https://bun.com/reference/node/inspector/Runtime/CallFrame)

      Function location.
    - [children](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode/children): [SamplingHeapProfileNode](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode)[]

      Child nodes.
    - [selfSize](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfileNode/selfSize): number

      Allocations size in bytes for the node excluding children.
  + ### interface [StartSamplingParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartSamplingParameterType)

    - [samplingInterval](https://bun.com/reference/node/inspector/HeapProfiler/StartSamplingParameterType/samplingInterval)?: number

      Average sample interval in bytes. Poisson distribution is used for the intervals. The default value is 32768 bytes.
  + ### interface [StartTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartTrackingHeapObjectsParameterType)

    - [trackAllocations](https://bun.com/reference/node/inspector/HeapProfiler/StartTrackingHeapObjectsParameterType/trackAllocations)?: boolean
  + ### interface [StopSamplingReturnType](https://bun.com/reference/node/inspector/HeapProfiler/StopSamplingReturnType)

    - [profile](https://bun.com/reference/node/inspector/HeapProfiler/StopSamplingReturnType/profile): [SamplingHeapProfile](https://bun.com/reference/node/inspector/HeapProfiler/SamplingHeapProfile)

      Recorded sampling heap profile.
  + ### interface [StopTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StopTrackingHeapObjectsParameterType)

    - [reportProgress](https://bun.com/reference/node/inspector/HeapProfiler/StopTrackingHeapObjectsParameterType/reportProgress)?: boolean

      If true 'reportHeapSnapshotProgress' events will be generated while snapshot is being taken when the tracking is stopped.
  + ### interface [TakeHeapSnapshotParameterType](https://bun.com/reference/node/inspector/HeapProfiler/TakeHeapSnapshotParameterType)

    - [reportProgress](https://bun.com/reference/node/inspector/HeapProfiler/TakeHeapSnapshotParameterType/reportProgress)?: boolean

      If true 'reportHeapSnapshotProgress' events will be generated while snapshot is being taken.
  + type [HeapSnapshotObjectId](https://bun.com/reference/node/inspector/HeapProfiler/HeapSnapshotObjectId) = string

    Heap snapshot object id.
* ### namespace [IO](https://bun.com/reference/node/inspector/IO)

  + ### interface [CloseParameterType](https://bun.com/reference/node/inspector/IO/CloseParameterType)

    - [handle](https://bun.com/reference/node/inspector/IO/CloseParameterType/handle): string

      Handle of the stream to close.
  + ### interface [ReadParameterType](https://bun.com/reference/node/inspector/IO/ReadParameterType)

    - [handle](https://bun.com/reference/node/inspector/IO/ReadParameterType/handle): string

      Handle of the stream to read.
    - [offset](https://bun.com/reference/node/inspector/IO/ReadParameterType/offset)?: number

      Seek to the specified offset before reading (if not specified, proceed with offset following the last read). Some types of streams may only support sequential reads.
    - [size](https://bun.com/reference/node/inspector/IO/ReadParameterType/size)?: number

      Maximum number of bytes to read (left upon the agent discretion if not specified).
  + ### interface [ReadReturnType](https://bun.com/reference/node/inspector/IO/ReadReturnType)

    - [data](https://bun.com/reference/node/inspector/IO/ReadReturnType/data): string

      Data that were read.
    - [eof](https://bun.com/reference/node/inspector/IO/ReadReturnType/eof): boolean

      Set if the end-of-file condition occurred while reading.
  + type [StreamHandle](https://bun.com/reference/node/inspector/IO/StreamHandle) = string
* ### namespace [NodeRuntime](https://bun.com/reference/node/inspector/NodeRuntime)

  + ### interface [NotifyWhenWaitingForDisconnectParameterType](https://bun.com/reference/node/inspector/NodeRuntime/NotifyWhenWaitingForDisconnectParameterType)

    - [enabled](https://bun.com/reference/node/inspector/NodeRuntime/NotifyWhenWaitingForDisconnectParameterType/enabled): boolean
* ### namespace [NodeTracing](https://bun.com/reference/node/inspector/NodeTracing)

  + ### interface [DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)

    - [value](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType/value): object[]
  + ### interface [GetCategoriesReturnType](https://bun.com/reference/node/inspector/NodeTracing/GetCategoriesReturnType)

    - [categories](https://bun.com/reference/node/inspector/NodeTracing/GetCategoriesReturnType/categories): string[]

      A list of supported tracing categories.
  + ### interface [StartParameterType](https://bun.com/reference/node/inspector/NodeTracing/StartParameterType)

    - [traceConfig](https://bun.com/reference/node/inspector/NodeTracing/StartParameterType/traceConfig): [TraceConfig](https://bun.com/reference/node/inspector/NodeTracing/TraceConfig)
  + ### interface [TraceConfig](https://bun.com/reference/node/inspector/NodeTracing/TraceConfig)

    - [includedCategories](https://bun.com/reference/node/inspector/NodeTracing/TraceConfig/includedCategories): string[]

      Included category filters.
    - [recordMode](https://bun.com/reference/node/inspector/NodeTracing/TraceConfig/recordMode)?: string

      Controls how the trace buffer stores data.
* ### namespace [NodeWorker](https://bun.com/reference/node/inspector/NodeWorker)

  + ### interface [AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)

    - [sessionId](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType/sessionId): string

      Identifier assigned to the session used to send/receive messages.
    - [waitingForDebugger](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType/waitingForDebugger): boolean
    - [workerInfo](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType/workerInfo): [WorkerInfo](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo)
  + ### interface [DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)

    - [sessionId](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType/sessionId): string

      Detached session identifier.
  + ### interface [DetachParameterType](https://bun.com/reference/node/inspector/NodeWorker/DetachParameterType)

    - [sessionId](https://bun.com/reference/node/inspector/NodeWorker/DetachParameterType/sessionId): string
  + ### interface [EnableParameterType](https://bun.com/reference/node/inspector/NodeWorker/EnableParameterType)

    - [waitForDebuggerOnStart](https://bun.com/reference/node/inspector/NodeWorker/EnableParameterType/waitForDebuggerOnStart): boolean

      Whether to new workers should be paused until the frontend sends `Runtime.runIfWaitingForDebugger` message to run them.
  + ### interface [ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)

    - [message](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType/message): string
    - [sessionId](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType/sessionId): string

      Identifier of a session which sends a message.
  + ### interface [SendMessageToWorkerParameterType](https://bun.com/reference/node/inspector/NodeWorker/SendMessageToWorkerParameterType)

    - [message](https://bun.com/reference/node/inspector/NodeWorker/SendMessageToWorkerParameterType/message): string
    - [sessionId](https://bun.com/reference/node/inspector/NodeWorker/SendMessageToWorkerParameterType/sessionId): string

      Identifier of the session.
  + ### interface [WorkerInfo](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo)

    - [title](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo/title): string
    - [type](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo/type): string
    - [url](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo/url): string
    - [workerId](https://bun.com/reference/node/inspector/NodeWorker/WorkerInfo/workerId): string
  + type [SessionID](https://bun.com/reference/node/inspector/NodeWorker/SessionID) = string

    Unique identifier of attached debugging session.
  + type [WorkerID](https://bun.com/reference/node/inspector/NodeWorker/WorkerID) = string
* ### namespace [Profiler](https://bun.com/reference/node/inspector/Profiler)

  + ### interface [ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)

    - [id](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType/id): string
    - [location](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location of console.profileEnd().
    - [profile](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType/profile): [Profile](https://bun.com/reference/node/inspector/Profiler/Profile)
    - [title](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType/title)?: string

      Profile title passed as an argument to console.profile().
  + ### interface [ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)

    - [id](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType/id): string
    - [location](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType/location): [Location](https://bun.com/reference/node/inspector/Debugger/Location)

      Location of console.profile().
    - [title](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType/title)?: string

      Profile title passed as an argument to console.profile().
  + ### interface [CoverageRange](https://bun.com/reference/node/inspector/Profiler/CoverageRange)

    Coverage data for a source range.

    - [count](https://bun.com/reference/node/inspector/Profiler/CoverageRange/count): number

      Collected execution count of the source range.
    - [endOffset](https://bun.com/reference/node/inspector/Profiler/CoverageRange/endOffset): number

      JavaScript script source offset for the range end.
    - [startOffset](https://bun.com/reference/node/inspector/Profiler/CoverageRange/startOffset): number

      JavaScript script source offset for the range start.
  + ### interface [FunctionCoverage](https://bun.com/reference/node/inspector/Profiler/FunctionCoverage)

    Coverage data for a JavaScript function.

    - [functionName](https://bun.com/reference/node/inspector/Profiler/FunctionCoverage/functionName): string

      JavaScript function name.
    - [isBlockCoverage](https://bun.com/reference/node/inspector/Profiler/FunctionCoverage/isBlockCoverage): boolean

      Whether coverage data for this function has block granularity.
    - [ranges](https://bun.com/reference/node/inspector/Profiler/FunctionCoverage/ranges): [CoverageRange](https://bun.com/reference/node/inspector/Profiler/CoverageRange)[]

      Source ranges inside the function with coverage data.
  + ### interface [GetBestEffortCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/GetBestEffortCoverageReturnType)

    - [result](https://bun.com/reference/node/inspector/Profiler/GetBestEffortCoverageReturnType/result): [ScriptCoverage](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage)[]

      Coverage data for the current isolate.
  + ### interface [PositionTickInfo](https://bun.com/reference/node/inspector/Profiler/PositionTickInfo)

    Specifies a number of samples attributed to a certain source position.

    - [line](https://bun.com/reference/node/inspector/Profiler/PositionTickInfo/line): number

      Source line number (1-based).
    - [ticks](https://bun.com/reference/node/inspector/Profiler/PositionTickInfo/ticks): number

      Number of samples attributed to the source line.
  + ### interface [Profile](https://bun.com/reference/node/inspector/Profiler/Profile)

    Profile.

    - [endTime](https://bun.com/reference/node/inspector/Profiler/Profile/endTime): number

      Profiling end timestamp in microseconds.
    - [nodes](https://bun.com/reference/node/inspector/Profiler/Profile/nodes): [ProfileNode](https://bun.com/reference/node/inspector/Profiler/ProfileNode)[]

      The list of profile nodes. First item is the root node.
    - [samples](https://bun.com/reference/node/inspector/Profiler/Profile/samples)?: number[]

      Ids of samples top nodes.
    - [startTime](https://bun.com/reference/node/inspector/Profiler/Profile/startTime): number

      Profiling start timestamp in microseconds.
    - [timeDeltas](https://bun.com/reference/node/inspector/Profiler/Profile/timeDeltas)?: number[]

      Time intervals between adjacent samples in microseconds. The first delta is relative to the profile startTime.
  + ### interface [ProfileNode](https://bun.com/reference/node/inspector/Profiler/ProfileNode)

    Profile node. Holds callsite information, execution statistics and child nodes.

    - [callFrame](https://bun.com/reference/node/inspector/Profiler/ProfileNode/callFrame): [CallFrame](https://bun.com/reference/node/inspector/Runtime/CallFrame)

      Function location.
    - [children](https://bun.com/reference/node/inspector/Profiler/ProfileNode/children)?: number[]

      Child node ids.
    - [deoptReason](https://bun.com/reference/node/inspector/Profiler/ProfileNode/deoptReason)?: string

      The reason of being not optimized. The function may be deoptimized or marked as don't optimize.
    - [hitCount](https://bun.com/reference/node/inspector/Profiler/ProfileNode/hitCount)?: number

      Number of samples where this node was on top of the call stack.
    - [id](https://bun.com/reference/node/inspector/Profiler/ProfileNode/id): number

      Unique id of the node.
    - [positionTicks](https://bun.com/reference/node/inspector/Profiler/ProfileNode/positionTicks)?: [PositionTickInfo](https://bun.com/reference/node/inspector/Profiler/PositionTickInfo)[]

      An array of source position ticks.
  + ### interface [ScriptCoverage](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage)

    Coverage data for a JavaScript script.

    - [functions](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage/functions): [FunctionCoverage](https://bun.com/reference/node/inspector/Profiler/FunctionCoverage)[]

      Functions contained in the script that has coverage data.
    - [scriptId](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage/scriptId): string

      JavaScript script id.
    - [url](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage/url): string

      JavaScript script name or url.
  + ### interface [SetSamplingIntervalParameterType](https://bun.com/reference/node/inspector/Profiler/SetSamplingIntervalParameterType)

    - [interval](https://bun.com/reference/node/inspector/Profiler/SetSamplingIntervalParameterType/interval): number

      New sampling interval in microseconds.
  + ### interface [StartPreciseCoverageParameterType](https://bun.com/reference/node/inspector/Profiler/StartPreciseCoverageParameterType)

    - [callCount](https://bun.com/reference/node/inspector/Profiler/StartPreciseCoverageParameterType/callCount)?: boolean

      Collect accurate call counts beyond simple 'covered' or 'not covered'.
    - [detailed](https://bun.com/reference/node/inspector/Profiler/StartPreciseCoverageParameterType/detailed)?: boolean

      Collect block-based coverage.
  + ### interface [StopReturnType](https://bun.com/reference/node/inspector/Profiler/StopReturnType)

    - [profile](https://bun.com/reference/node/inspector/Profiler/StopReturnType/profile): [Profile](https://bun.com/reference/node/inspector/Profiler/Profile)

      Recorded profile.
  + ### interface [TakePreciseCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/TakePreciseCoverageReturnType)

    - [result](https://bun.com/reference/node/inspector/Profiler/TakePreciseCoverageReturnType/result): [ScriptCoverage](https://bun.com/reference/node/inspector/Profiler/ScriptCoverage)[]

      Coverage data for the current isolate.
* ### namespace [Runtime](https://bun.com/reference/node/inspector/Runtime)

  + ### interface [AwaitPromiseParameterType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType)

    - [generatePreview](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType/generatePreview)?: boolean

      Whether preview should be generated for the result.
    - [promiseObjectId](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType/promiseObjectId): string

      Identifier of the promise.
    - [returnByValue](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType/returnByValue)?: boolean

      Whether the result is expected to be a JSON object that should be sent by value.
  + ### interface [AwaitPromiseReturnType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details if stack strace is available.
    - [result](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Promise result. Will contain rejected value if promise was rejected.
  + ### interface [CallArgument](https://bun.com/reference/node/inspector/Runtime/CallArgument)

    Represents function call argument. Either remote object id <code>objectId</code>, primitive <code>value</code>, unserializable primitive value or neither of (for undefined) them should be specified.

    - [objectId](https://bun.com/reference/node/inspector/Runtime/CallArgument/objectId)?: string

      Remote object handle.
    - [unserializableValue](https://bun.com/reference/node/inspector/Runtime/CallArgument/unserializableValue)?: string

      Primitive value which can not be JSON-stringified.
    - [value](https://bun.com/reference/node/inspector/Runtime/CallArgument/value)?: any

      Primitive value or serializable javascript object.
  + ### interface [CallFrame](https://bun.com/reference/node/inspector/Runtime/CallFrame)

    Stack entry for runtime errors and assertions.

    - [columnNumber](https://bun.com/reference/node/inspector/Runtime/CallFrame/columnNumber): number

      JavaScript script column number (0-based).
    - [functionName](https://bun.com/reference/node/inspector/Runtime/CallFrame/functionName): string

      JavaScript function name.
    - [lineNumber](https://bun.com/reference/node/inspector/Runtime/CallFrame/lineNumber): number

      JavaScript script line number (0-based).
    - [scriptId](https://bun.com/reference/node/inspector/Runtime/CallFrame/scriptId): string

      JavaScript script id.
    - [url](https://bun.com/reference/node/inspector/Runtime/CallFrame/url): string

      JavaScript script name or url.
  + ### interface [CallFunctionOnParameterType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType)

    - [arguments](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/arguments)?: [CallArgument](https://bun.com/reference/node/inspector/Runtime/CallArgument)[]

      Call arguments. All call arguments must belong to the same JavaScript world as the target object.
    - [awaitPromise](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/awaitPromise)?: boolean

      Whether execution should <code>await</code> for resulting value and return once awaited promise is resolved.
    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/executionContextId)?: number

      Specifies execution context which global object will be used to call function on. Either executionContextId or objectId should be specified.
    - [functionDeclaration](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/functionDeclaration): string

      Declaration of the function to call.
    - [generatePreview](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/generatePreview)?: boolean

      Whether preview should be generated for the result.
    - [objectGroup](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/objectGroup)?: string

      Symbolic group name that can be used to release multiple objects. If objectGroup is not specified and objectId is, objectGroup will be inherited from object.
    - [objectId](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/objectId)?: string

      Identifier of the object to call function on. Either objectId or executionContextId should be specified.
    - [returnByValue](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/returnByValue)?: boolean

      Whether the result is expected to be a JSON object which should be sent by value.
    - [silent](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/silent)?: boolean

      In silent mode exceptions thrown during evaluation are not reported and do not pause execution. Overrides <code>setPauseOnException</code> state.
    - [userGesture](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType/userGesture)?: boolean

      Whether execution should be treated as initiated by user in the UI.
  + ### interface [CallFunctionOnReturnType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [result](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Call result.
  + ### interface [CompileScriptParameterType](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType)

    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType/executionContextId)?: number

      Specifies in which execution context to perform script run. If the parameter is omitted the evaluation will be performed in the context of the inspected page.
    - [expression](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType/expression): string

      Expression to compile.
    - [persistScript](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType/persistScript): boolean

      Specifies whether the compiled script should be persisted.
    - [sourceURL](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType/sourceURL): string

      Source url to be set for the script.
  + ### interface [CompileScriptReturnType](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [scriptId](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType/scriptId)?: string

      Id of the script.
  + ### interface [ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)

    - [args](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/args): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)[]

      Call arguments.
    - [context](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/context)?: string

      Console context descriptor for calls on non-default console context (not console.\*): 'anonymous#unique-logger-id' for call on unnamed context, 'name#unique-logger-id' for call on named context.
    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/executionContextId): number

      Identifier of the context where the call was made.
    - [stackTrace](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/stackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Stack trace captured when the call was made.
    - [timestamp](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/timestamp): number

      Call timestamp.
    - [type](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType/type): string

      Type of the call.
  + ### interface [CustomPreview](https://bun.com/reference/node/inspector/Runtime/CustomPreview)

    - [bindRemoteObjectFunctionId](https://bun.com/reference/node/inspector/Runtime/CustomPreview/bindRemoteObjectFunctionId): string
    - [configObjectId](https://bun.com/reference/node/inspector/Runtime/CustomPreview/configObjectId)?: string
    - [formatterObjectId](https://bun.com/reference/node/inspector/Runtime/CustomPreview/formatterObjectId): string
    - [hasBody](https://bun.com/reference/node/inspector/Runtime/CustomPreview/hasBody): boolean
    - [header](https://bun.com/reference/node/inspector/Runtime/CustomPreview/header): string
  + ### interface [EntryPreview](https://bun.com/reference/node/inspector/Runtime/EntryPreview)

    - [key](https://bun.com/reference/node/inspector/Runtime/EntryPreview/key)?: [ObjectPreview](https://bun.com/reference/node/inspector/Runtime/ObjectPreview)

      Preview of the key. Specified for map-like collection entries.
    - [value](https://bun.com/reference/node/inspector/Runtime/EntryPreview/value): [ObjectPreview](https://bun.com/reference/node/inspector/Runtime/ObjectPreview)

      Preview of the value.
  + ### interface [EvaluateParameterType](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType)

    - [awaitPromise](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/awaitPromise)?: boolean

      Whether execution should <code>await</code> for resulting value and return once awaited promise is resolved.
    - [contextId](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/contextId)?: number

      Specifies in which execution context to perform evaluation. If the parameter is omitted the evaluation will be performed in the context of the inspected page.
    - [expression](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/expression): string

      Expression to evaluate.
    - [generatePreview](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/generatePreview)?: boolean

      Whether preview should be generated for the result.
    - [includeCommandLineAPI](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/includeCommandLineAPI)?: boolean

      Determines whether Command Line API should be available during the evaluation.
    - [objectGroup](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/objectGroup)?: string

      Symbolic group name that can be used to release multiple objects.
    - [returnByValue](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/returnByValue)?: boolean

      Whether the result is expected to be a JSON object that should be sent by value.
    - [silent](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/silent)?: boolean

      In silent mode exceptions thrown during evaluation are not reported and do not pause execution. Overrides <code>setPauseOnException</code> state.
    - [userGesture](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType/userGesture)?: boolean

      Whether execution should be treated as initiated by user in the UI.
  + ### interface [EvaluateReturnType](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [result](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Evaluation result.
  + ### interface [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

    Detailed information about exception (or error) that was thrown during script compilation or execution.

    - [columnNumber](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/columnNumber): number

      Column number of the exception location (0-based).
    - [exception](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/exception)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Exception object if available.
    - [exceptionId](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/exceptionId): number

      Exception id.
    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/executionContextId)?: number

      Identifier of the context where exception happened.
    - [lineNumber](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/lineNumber): number

      Line number of the exception location (0-based).
    - [scriptId](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/scriptId)?: string

      Script ID of the exception location.
    - [stackTrace](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/stackTrace)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      JavaScript stack trace if available.
    - [text](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/text): string

      Exception text, which should be used together with exception object when available.
    - [url](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails/url)?: string

      URL of the exception location, to be used when the script was not reported.
  + ### interface [ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)

    - [exceptionId](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType/exceptionId): number

      The id of revoked exception, as reported in <code>exceptionThrown</code>.
    - [reason](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType/reason): string

      Reason describing why exception was revoked.
  + ### interface [ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType/exceptionDetails): [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)
    - [timestamp](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType/timestamp): number

      Timestamp of the exception.
  + ### interface [ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)

    - [context](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType/context): [ExecutionContextDescription](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription)

      A newly created execution context.
  + ### interface [ExecutionContextDescription](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription)

    Description of an isolated world.

    - [auxData](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription/auxData)?: object

      Embedder-specific auxiliary data.
    - [id](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription/id): number

      Unique id of the execution context. It can be used to specify in which execution context script evaluation should be performed.
    - [name](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription/name): string

      Human readable name describing given context.
    - [origin](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDescription/origin): string

      Execution context origin.
  + ### interface [ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)

    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType/executionContextId): number

      Id of the destroyed context
  + ### interface [GetPropertiesParameterType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType)

    - [accessorPropertiesOnly](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType/accessorPropertiesOnly)?: boolean

      If true, returns accessor properties (with getter/setter) only; internal properties are not returned either.
    - [generatePreview](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType/generatePreview)?: boolean

      Whether preview should be generated for the results.
    - [objectId](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType/objectId): string

      Identifier of the object to return properties for.
    - [ownProperties](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType/ownProperties)?: boolean

      If true, returns properties belonging only to the element itself, not to its prototype chain.
  + ### interface [GetPropertiesReturnType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [internalProperties](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType/internalProperties)?: [InternalPropertyDescriptor](https://bun.com/reference/node/inspector/Runtime/InternalPropertyDescriptor)[]

      Internal object properties (only of the element itself).
    - [result](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType/result): [PropertyDescriptor](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor)[]

      Object properties.
  + ### interface [GlobalLexicalScopeNamesParameterType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesParameterType)

    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesParameterType/executionContextId)?: number

      Specifies in which execution context to lookup global scope variables.
  + ### interface [GlobalLexicalScopeNamesReturnType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesReturnType)

    - [names](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesReturnType/names): string[]
  + ### interface [InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)

    - [hints](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType/hints): object
    - [object](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType/object): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)
  + ### interface [InternalPropertyDescriptor](https://bun.com/reference/node/inspector/Runtime/InternalPropertyDescriptor)

    Object internal property descriptor. This property isn't normally visible in JavaScript code.

    - [name](https://bun.com/reference/node/inspector/Runtime/InternalPropertyDescriptor/name): string

      Conventional property name.
    - [value](https://bun.com/reference/node/inspector/Runtime/InternalPropertyDescriptor/value)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      The value associated with the property.
  + ### interface [ObjectPreview](https://bun.com/reference/node/inspector/Runtime/ObjectPreview)

    Object containing abbreviated remote object value.

    - [description](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/description)?: string

      String representation of the object.
    - [entries](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/entries)?: [EntryPreview](https://bun.com/reference/node/inspector/Runtime/EntryPreview)[]

      List of the entries. Specified for <code>map</code> and <code>set</code> subtype values only.
    - [overflow](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/overflow): boolean

      True iff some of the properties or entries of the original object did not fit.
    - [properties](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/properties): [PropertyPreview](https://bun.com/reference/node/inspector/Runtime/PropertyPreview)[]

      List of the properties.
    - [subtype](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/subtype)?: string

      Object subtype hint. Specified for <code>object</code> type values only.
    - [type](https://bun.com/reference/node/inspector/Runtime/ObjectPreview/type): string

      Object type.
  + ### interface [PropertyDescriptor](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor)

    Object property descriptor.

    - [configurable](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/configurable): boolean

      True if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.
    - [enumerable](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/enumerable): boolean

      True if this property shows up during enumeration of the properties on the corresponding object.
    - [get](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/get)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      A function which serves as a getter for the property, or <code>undefined</code> if there is no getter (accessor descriptors only).
    - [isOwn](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/isOwn)?: boolean

      True if the property is owned for the object.
    - [name](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/name): string

      Property name or symbol description.
    - [set](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/set)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      A function which serves as a setter for the property, or <code>undefined</code> if there is no setter (accessor descriptors only).
    - [symbol](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/symbol)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Property symbol object, if the property is of the <code>symbol</code> type.
    - [value](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/value)?: [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      The value associated with the property.
    - [wasThrown](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/wasThrown)?: boolean

      True if the result was thrown during the evaluation.
    - [writable](https://bun.com/reference/node/inspector/Runtime/PropertyDescriptor/writable)?: boolean

      True if the value associated with the property may be changed (data descriptors only).
  + ### interface [PropertyPreview](https://bun.com/reference/node/inspector/Runtime/PropertyPreview)

    - [name](https://bun.com/reference/node/inspector/Runtime/PropertyPreview/name): string

      Property name.
    - [subtype](https://bun.com/reference/node/inspector/Runtime/PropertyPreview/subtype)?: string

      Object subtype hint. Specified for <code>object</code> type values only.
    - [type](https://bun.com/reference/node/inspector/Runtime/PropertyPreview/type): string

      Object type. Accessor means that the property itself is an accessor property.
    - [value](https://bun.com/reference/node/inspector/Runtime/PropertyPreview/value)?: string

      User-friendly property value string.
    - [valuePreview](https://bun.com/reference/node/inspector/Runtime/PropertyPreview/valuePreview)?: [ObjectPreview](https://bun.com/reference/node/inspector/Runtime/ObjectPreview)

      Nested value preview.
  + ### interface [QueryObjectsParameterType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsParameterType)

    - [prototypeObjectId](https://bun.com/reference/node/inspector/Runtime/QueryObjectsParameterType/prototypeObjectId): string

      Identifier of the prototype to return objects for.
  + ### interface [QueryObjectsReturnType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsReturnType)

    - [objects](https://bun.com/reference/node/inspector/Runtime/QueryObjectsReturnType/objects): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Array with objects.
  + ### interface [ReleaseObjectGroupParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectGroupParameterType)

    - [objectGroup](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectGroupParameterType/objectGroup): string

      Symbolic object group name.
  + ### interface [ReleaseObjectParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectParameterType)

    - [objectId](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectParameterType/objectId): string

      Identifier of the object to release.
  + ### interface [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

    Mirror object referencing original JavaScript object.

    - [className](https://bun.com/reference/node/inspector/Runtime/RemoteObject/className)?: string

      Object class (constructor) name. Specified for <code>object</code> type values only.
    - [customPreview](https://bun.com/reference/node/inspector/Runtime/RemoteObject/customPreview)?: [CustomPreview](https://bun.com/reference/node/inspector/Runtime/CustomPreview)
    - [description](https://bun.com/reference/node/inspector/Runtime/RemoteObject/description)?: string

      String representation of the object.
    - [objectId](https://bun.com/reference/node/inspector/Runtime/RemoteObject/objectId)?: string

      Unique object identifier (for non-primitive values).
    - [preview](https://bun.com/reference/node/inspector/Runtime/RemoteObject/preview)?: [ObjectPreview](https://bun.com/reference/node/inspector/Runtime/ObjectPreview)

      Preview containing abbreviated property values. Specified for <code>object</code> type values only.
    - [subtype](https://bun.com/reference/node/inspector/Runtime/RemoteObject/subtype)?: string

      Object subtype hint. Specified for <code>object</code> type values only.
    - [type](https://bun.com/reference/node/inspector/Runtime/RemoteObject/type): string

      Object type.
    - [unserializableValue](https://bun.com/reference/node/inspector/Runtime/RemoteObject/unserializableValue)?: string

      Primitive value which can not be JSON-stringified does not have <code>value</code>, but gets this property.
    - [value](https://bun.com/reference/node/inspector/Runtime/RemoteObject/value)?: any

      Remote object value in case of primitive values or JSON values (if it was requested).
  + ### interface [RunScriptParameterType](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType)

    - [awaitPromise](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/awaitPromise)?: boolean

      Whether execution should <code>await</code> for resulting value and return once awaited promise is resolved.
    - [executionContextId](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/executionContextId)?: number

      Specifies in which execution context to perform script run. If the parameter is omitted the evaluation will be performed in the context of the inspected page.
    - [generatePreview](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/generatePreview)?: boolean

      Whether preview should be generated for the result.
    - [includeCommandLineAPI](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/includeCommandLineAPI)?: boolean

      Determines whether Command Line API should be available during the evaluation.
    - [objectGroup](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/objectGroup)?: string

      Symbolic group name that can be used to release multiple objects.
    - [returnByValue](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/returnByValue)?: boolean

      Whether the result is expected to be a JSON object which should be sent by value.
    - [scriptId](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/scriptId): string

      Id of the script to run.
    - [silent](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType/silent)?: boolean

      In silent mode exceptions thrown during evaluation are not reported and do not pause execution. Overrides <code>setPauseOnException</code> state.
  + ### interface [RunScriptReturnType](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType)

    - [exceptionDetails](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType/exceptionDetails)?: [ExceptionDetails](https://bun.com/reference/node/inspector/Runtime/ExceptionDetails)

      Exception details.
    - [result](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType/result): [RemoteObject](https://bun.com/reference/node/inspector/Runtime/RemoteObject)

      Run result.
  + ### interface [SetCustomObjectFormatterEnabledParameterType](https://bun.com/reference/node/inspector/Runtime/SetCustomObjectFormatterEnabledParameterType)

    - [enabled](https://bun.com/reference/node/inspector/Runtime/SetCustomObjectFormatterEnabledParameterType/enabled): boolean
  + ### interface [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

    Call frames for assertions or error messages.

    - [callFrames](https://bun.com/reference/node/inspector/Runtime/StackTrace/callFrames): [CallFrame](https://bun.com/reference/node/inspector/Runtime/CallFrame)[]

      JavaScript function name.
    - [description](https://bun.com/reference/node/inspector/Runtime/StackTrace/description)?: string

      String label of this stack trace. For async traces this may be a name of the function that initiated the async call.
    - [parent](https://bun.com/reference/node/inspector/Runtime/StackTrace/parent)?: [StackTrace](https://bun.com/reference/node/inspector/Runtime/StackTrace)

      Asynchronous JavaScript stack trace that preceded this stack, if available.
    - [parentId](https://bun.com/reference/node/inspector/Runtime/StackTrace/parentId)?: [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

      Asynchronous JavaScript stack trace that preceded this stack, if available.
  + ### interface [StackTraceId](https://bun.com/reference/node/inspector/Runtime/StackTraceId)

    If <code>debuggerId</code> is set stack trace comes from another debugger and can be resolved there. This allows to track cross-debugger calls. See <code>Runtime.StackTrace</code> and <code>Debugger.paused</code> for usages.

    - [debuggerId](https://bun.com/reference/node/inspector/Runtime/StackTraceId/debuggerId)?: string
    - [id](https://bun.com/reference/node/inspector/Runtime/StackTraceId/id): string
  + type [ExecutionContextId](https://bun.com/reference/node/inspector/Runtime/ExecutionContextId) = number

    Id of an execution context.
  + type [RemoteObjectId](https://bun.com/reference/node/inspector/Runtime/RemoteObjectId) = string

    Unique object identifier.
  + type [ScriptId](https://bun.com/reference/node/inspector/Runtime/ScriptId) = string

    Unique script identifier.
  + type [Timestamp](https://bun.com/reference/node/inspector/Runtime/Timestamp) = number

    Number of milliseconds since epoch.
  + type [UniqueDebuggerId](https://bun.com/reference/node/inspector/Runtime/UniqueDebuggerId) = string

    Unique identifier of current debugger.
  + type [UnserializableValue](https://bun.com/reference/node/inspector/Runtime/UnserializableValue) = string

    Primitive value which cannot be JSON-stringified.
* ### namespace [Schema](https://bun.com/reference/node/inspector/Schema)

  + ### interface [Domain](https://bun.com/reference/node/inspector/Schema/Domain)

    Description of the protocol domain.

    - [name](https://bun.com/reference/node/inspector/Schema/Domain/name): string

      Domain name.
    - [version](https://bun.com/reference/node/inspector/Schema/Domain/version): string

      Domain version.
  + ### interface [GetDomainsReturnType](https://bun.com/reference/node/inspector/Schema/GetDomainsReturnType)

    - [domains](https://bun.com/reference/node/inspector/Schema/GetDomainsReturnType/domains): [Domain](https://bun.com/reference/node/inspector/Schema/Domain)[]

      List of supported domains.
* ### namespace [Target](https://bun.com/reference/node/inspector/Target)

  + ### interface [AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)

    - [sessionId](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType/sessionId): string
    - [targetInfo](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType/targetInfo): [TargetInfo](https://bun.com/reference/node/inspector/Target/TargetInfo)
    - [waitingForDebugger](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType/waitingForDebugger): boolean
  + ### interface [SetAutoAttachParameterType](https://bun.com/reference/node/inspector/Target/SetAutoAttachParameterType)

    - [autoAttach](https://bun.com/reference/node/inspector/Target/SetAutoAttachParameterType/autoAttach): boolean
    - [waitForDebuggerOnStart](https://bun.com/reference/node/inspector/Target/SetAutoAttachParameterType/waitForDebuggerOnStart): boolean
  + ### interface [TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)

    - [targetInfo](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType/targetInfo): [TargetInfo](https://bun.com/reference/node/inspector/Target/TargetInfo)
  + ### interface [TargetInfo](https://bun.com/reference/node/inspector/Target/TargetInfo)

    - [attached](https://bun.com/reference/node/inspector/Target/TargetInfo/attached): boolean
    - [canAccessOpener](https://bun.com/reference/node/inspector/Target/TargetInfo/canAccessOpener): boolean
    - [targetId](https://bun.com/reference/node/inspector/Target/TargetInfo/targetId): string
    - [title](https://bun.com/reference/node/inspector/Target/TargetInfo/title): string
    - [type](https://bun.com/reference/node/inspector/Target/TargetInfo/type): string
    - [url](https://bun.com/reference/node/inspector/Target/TargetInfo/url): string
  + type [SessionID](https://bun.com/reference/node/inspector/Target/SessionID) = string
  + type [TargetID](https://bun.com/reference/node/inspector/Target/TargetID) = string
* ### interface [InspectorConsole](https://bun.com/reference/node/inspector/InspectorConsole)

  + [assert](https://bun.com/reference/node/inspector/InspectorConsole/assert)(

    value?: any,

    ...data: any[]

    ): void;
  + [clear](https://bun.com/reference/node/inspector/InspectorConsole/clear)(

    ...data: any[]

    ): void;
  + [count](https://bun.com/reference/node/inspector/InspectorConsole/count)(

    label?: any

    ): void;
  + [countReset](https://bun.com/reference/node/inspector/InspectorConsole/countReset)(

    label?: any

    ): void;
  + [debug](https://bun.com/reference/node/inspector/InspectorConsole/debug)(

    ...data: any[]

    ): void;
  + [dir](https://bun.com/reference/node/inspector/InspectorConsole/dir)(

    ...data: any[]

    ): void;
  + [dirxml](https://bun.com/reference/node/inspector/InspectorConsole/dirxml)(

    ...data: any[]

    ): void;
  + [error](https://bun.com/reference/node/inspector/InspectorConsole/error)(

    ...data: any[]

    ): void;
  + [group](https://bun.com/reference/node/inspector/InspectorConsole/group)(

    ...data: any[]

    ): void;
  + [groupCollapsed](https://bun.com/reference/node/inspector/InspectorConsole/groupCollapsed)(

    ...data: any[]

    ): void;
  + [groupEnd](https://bun.com/reference/node/inspector/InspectorConsole/groupEnd)(

    ...data: any[]

    ): void;
  + [info](https://bun.com/reference/node/inspector/InspectorConsole/info)(

    ...data: any[]

    ): void;
  + [log](https://bun.com/reference/node/inspector/InspectorConsole/log)(

    ...data: any[]

    ): void;
  + [profile](https://bun.com/reference/node/inspector/InspectorConsole/profile)(

    label?: any

    ): void;
  + [profileEnd](https://bun.com/reference/node/inspector/InspectorConsole/profileEnd)(

    label?: any

    ): void;
  + [table](https://bun.com/reference/node/inspector/InspectorConsole/table)(

    ...data: any[]

    ): void;
  + [time](https://bun.com/reference/node/inspector/InspectorConsole/time)(

    label?: any

    ): void;
  + [timeLog](https://bun.com/reference/node/inspector/InspectorConsole/timeLog)(

    label?: any

    ): void;
  + [timeStamp](https://bun.com/reference/node/inspector/InspectorConsole/timeStamp)(

    label?: any

    ): void;
  + [trace](https://bun.com/reference/node/inspector/InspectorConsole/trace)(

    ...data: any[]

    ): void;
  + [warn](https://bun.com/reference/node/inspector/InspectorConsole/warn)(

    ...data: any[]

    ): void;
* ### interface [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<T>

  + [method](https://bun.com/reference/node/inspector/InspectorNotification/method): string
  + [params](https://bun.com/reference/node/inspector/InspectorNotification/params): T