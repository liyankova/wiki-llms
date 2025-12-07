---
url: https://bun.com/reference/node/inspector/promises
title: Node.js inspector/promises module | API Reference | Bun
source_domain: bun.com
---

# Node.js inspector/promises module | API Reference | Bun

Node.js module

# [inspector/promises](https://bun.com/reference/node/inspector/promises)

* ### class [Session](https://bun.com/reference/node/inspector/promises/Session)

  The `inspector.Session` is used for dispatching messages to the V8 inspector back-end and receiving message responses and notifications.

  + static [captureRejections](https://bun.com/reference/node/inspector/promises/Session/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/inspector/promises/Session/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/inspector/promises/Session/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/inspector/promises/Session/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/inspector/promises/Session/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [addListener](https://bun.com/reference/node/inspector/promises/Session/addListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [connect](https://bun.com/reference/node/inspector/promises/Session/connect)(): void;

    Connects a session to the inspector back-end.
  + [connectToMainThread](https://bun.com/reference/node/inspector/promises/Session/connectToMainThread)(): void;

    Connects a session to the inspector back-end. An exception will be thrown if this API was not called on a Worker thread.
  + [disconnect](https://bun.com/reference/node/inspector/promises/Session/disconnect)(): void;

    Immediately close the session. All pending message callbacks will be called with an error. `session.connect()` will need to be called to be able to send messages again. Reconnected session will lose all inspector state, such as enabled agents or configured breakpoints.
  + [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

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

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'inspectorNotification',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.executionContextCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.executionContextDestroyed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.executionContextsCleared'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.exceptionThrown',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.exceptionRevoked',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.consoleAPICalled',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Runtime.inspectRequested',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Debugger.scriptParsed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Debugger.scriptFailedToParse',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Debugger.breakpointResolved',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Debugger.paused',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Debugger.resumed'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Console.messageAdded',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Profiler.consoleProfileStarted',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Profiler.consoleProfileFinished',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'HeapProfiler.resetProfiles'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'HeapProfiler.lastSeenObjectId',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'HeapProfiler.heapStatsUpdate',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeTracing.dataCollected',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeTracing.tracingComplete'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeWorker.attachedToWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeWorker.detachedFromWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeWorker.receivedMessageFromWorker',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.requestWillBeSent',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.responseReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.loadingFailed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.loadingFinished',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.dataReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.webSocketCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.webSocketClosed',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Network.webSocketHandshakeResponseReceived',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeRuntime.waitingForDisconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'NodeRuntime.waitingForDebugger'

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Target.targetCreated',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>

    ): boolean;

    [emit](https://bun.com/reference/node/inspector/promises/Session/emit)(

    event: 'Target.attachedToTarget',

    message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>

    ): boolean;
  + [eventNames](https://bun.com/reference/node/inspector/promises/Session/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/inspector/promises/Session/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/inspector/promises/Session/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/inspector/promises/Session/listeners)<K>(

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
  + [off](https://bun.com/reference/node/inspector/promises/Session/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/inspector/promises/Session/on)(

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

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [on](https://bun.com/reference/node/inspector/promises/Session/on)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [once](https://bun.com/reference/node/inspector/promises/Session/once)(

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

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [once](https://bun.com/reference/node/inspector/promises/Session/once)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: string,

    params?: object

    ): Promise<void>;

    Posts a message to the inspector back-end.

    ```
    import { Session } from 'node:inspector/promises';
    try {
      const session = new Session();
      session.connect();
      const result = await session.post('Runtime.evaluate', { expression: '2 + 2' });
      console.log(result);
    } catch (error) {
      console.error(error);
    }
    // Output: { result: { type: 'number', value: 4, description: '4' } }
    ```

    The latest version of the V8 inspector protocol is published on the [Chrome DevTools Protocol Viewer](https://chromedevtools.github.io/devtools-protocol/v8/).

    Node.js inspector supports all the Chrome DevTools Protocol domains declared by V8. Chrome DevTools Protocol domain provides an interface for interacting with one of the runtime agents used to inspect the application state and listen to the run-time events.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Schema.getDomains'

    ): Promise<[GetDomainsReturnType](https://bun.com/reference/node/inspector/Schema/GetDomainsReturnType)>;

    Returns supported domains.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.evaluate',

    params?: [EvaluateParameterType](https://bun.com/reference/node/inspector/Runtime/EvaluateParameterType)

    ): Promise<[EvaluateReturnType](https://bun.com/reference/node/inspector/Runtime/EvaluateReturnType)>;

    Evaluates expression on global object.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.awaitPromise',

    params?: [AwaitPromiseParameterType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseParameterType)

    ): Promise<[AwaitPromiseReturnType](https://bun.com/reference/node/inspector/Runtime/AwaitPromiseReturnType)>;

    Add handler to promise with given promise object id.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.callFunctionOn',

    params?: [CallFunctionOnParameterType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnParameterType)

    ): Promise<[CallFunctionOnReturnType](https://bun.com/reference/node/inspector/Runtime/CallFunctionOnReturnType)>;

    Calls function with given declaration on the given object. Object group of the result is inherited from the target object.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.getProperties',

    params?: [GetPropertiesParameterType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesParameterType)

    ): Promise<[GetPropertiesReturnType](https://bun.com/reference/node/inspector/Runtime/GetPropertiesReturnType)>;

    Returns properties of a given object. Object group of the result is inherited from the target object.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.releaseObject',

    params?: [ReleaseObjectParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectParameterType)

    ): Promise<void>;

    Releases remote object with given id.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.releaseObjectGroup',

    params?: [ReleaseObjectGroupParameterType](https://bun.com/reference/node/inspector/Runtime/ReleaseObjectGroupParameterType)

    ): Promise<void>;

    Releases all remote objects that belong to a given group.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.runIfWaitingForDebugger'

    ): Promise<void>;

    Tells inspected instance to run if it was waiting for debugger to attach.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.enable'

    ): Promise<void>;

    Enables reporting of execution contexts creation by means of <code>executionContextCreated</code> event. When the reporting gets enabled the event will be sent immediately for each existing execution context.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.disable'

    ): Promise<void>;

    Disables reporting of execution contexts creation.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.discardConsoleEntries'

    ): Promise<void>;

    Discards collected exceptions and console API calls.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.setCustomObjectFormatterEnabled',

    params?: [SetCustomObjectFormatterEnabledParameterType](https://bun.com/reference/node/inspector/Runtime/SetCustomObjectFormatterEnabledParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.compileScript',

    params?: [CompileScriptParameterType](https://bun.com/reference/node/inspector/Runtime/CompileScriptParameterType)

    ): Promise<[CompileScriptReturnType](https://bun.com/reference/node/inspector/Runtime/CompileScriptReturnType)>;

    Compiles expression.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.runScript',

    params?: [RunScriptParameterType](https://bun.com/reference/node/inspector/Runtime/RunScriptParameterType)

    ): Promise<[RunScriptReturnType](https://bun.com/reference/node/inspector/Runtime/RunScriptReturnType)>;

    Runs script with given id in a given context.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.queryObjects',

    params?: [QueryObjectsParameterType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsParameterType)

    ): Promise<[QueryObjectsReturnType](https://bun.com/reference/node/inspector/Runtime/QueryObjectsReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Runtime.globalLexicalScopeNames',

    params?: [GlobalLexicalScopeNamesParameterType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesParameterType)

    ): Promise<[GlobalLexicalScopeNamesReturnType](https://bun.com/reference/node/inspector/Runtime/GlobalLexicalScopeNamesReturnType)>;

    Returns all let, const and class variables from global scope.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.enable'

    ): Promise<[EnableReturnType](https://bun.com/reference/node/inspector/Debugger/EnableReturnType)>;

    Enables debugger for the given page. Clients should not assume that the debugging has been enabled until the result for this command is received.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.disable'

    ): Promise<void>;

    Disables debugger for given page.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setBreakpointsActive',

    params?: [SetBreakpointsActiveParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointsActiveParameterType)

    ): Promise<void>;

    Activates / deactivates all breakpoints on the page.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setSkipAllPauses',

    params?: [SetSkipAllPausesParameterType](https://bun.com/reference/node/inspector/Debugger/SetSkipAllPausesParameterType)

    ): Promise<void>;

    Makes page not interrupt on any pauses (breakpoint, exception, dom exception etc).

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setBreakpointByUrl',

    params?: [SetBreakpointByUrlParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlParameterType)

    ): Promise<[SetBreakpointByUrlReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointByUrlReturnType)>;

    Sets JavaScript breakpoint at given location specified either by URL or URL regex. Once this command is issued, all existing parsed scripts will have breakpoints resolved and returned in <code>locations</code> property. Further matching script parsing will result in subsequent <code>breakpointResolved</code> events issued. This logical breakpoint will survive page reloads.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setBreakpoint',

    params?: [SetBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointParameterType)

    ): Promise<[SetBreakpointReturnType](https://bun.com/reference/node/inspector/Debugger/SetBreakpointReturnType)>;

    Sets JavaScript breakpoint at a given location.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.removeBreakpoint',

    params?: [RemoveBreakpointParameterType](https://bun.com/reference/node/inspector/Debugger/RemoveBreakpointParameterType)

    ): Promise<void>;

    Removes JavaScript breakpoint.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.getPossibleBreakpoints',

    params?: [GetPossibleBreakpointsParameterType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsParameterType)

    ): Promise<[GetPossibleBreakpointsReturnType](https://bun.com/reference/node/inspector/Debugger/GetPossibleBreakpointsReturnType)>;

    Returns possible locations for breakpoint. scriptId in start and end range locations should be the same.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.continueToLocation',

    params?: [ContinueToLocationParameterType](https://bun.com/reference/node/inspector/Debugger/ContinueToLocationParameterType)

    ): Promise<void>;

    Continues execution until specific location is reached.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.pauseOnAsyncCall',

    params?: [PauseOnAsyncCallParameterType](https://bun.com/reference/node/inspector/Debugger/PauseOnAsyncCallParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.stepOver'

    ): Promise<void>;

    Steps over the statement.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.stepInto',

    params?: [StepIntoParameterType](https://bun.com/reference/node/inspector/Debugger/StepIntoParameterType)

    ): Promise<void>;

    Steps into the function call.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.stepOut'

    ): Promise<void>;

    Steps out of the function call.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.pause'

    ): Promise<void>;

    Stops on the next JavaScript statement.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.resume'

    ): Promise<void>;

    Resumes JavaScript execution.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.getStackTrace',

    params?: [GetStackTraceParameterType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceParameterType)

    ): Promise<[GetStackTraceReturnType](https://bun.com/reference/node/inspector/Debugger/GetStackTraceReturnType)>;

    Returns stack trace with given <code>stackTraceId</code>.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.searchInContent',

    params?: [SearchInContentParameterType](https://bun.com/reference/node/inspector/Debugger/SearchInContentParameterType)

    ): Promise<[SearchInContentReturnType](https://bun.com/reference/node/inspector/Debugger/SearchInContentReturnType)>;

    Searches for given string in script content.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setScriptSource',

    params?: [SetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceParameterType)

    ): Promise<[SetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/SetScriptSourceReturnType)>;

    Edits JavaScript source live.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.restartFrame',

    params?: [RestartFrameParameterType](https://bun.com/reference/node/inspector/Debugger/RestartFrameParameterType)

    ): Promise<[RestartFrameReturnType](https://bun.com/reference/node/inspector/Debugger/RestartFrameReturnType)>;

    Restarts particular call frame from the beginning.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.getScriptSource',

    params?: [GetScriptSourceParameterType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceParameterType)

    ): Promise<[GetScriptSourceReturnType](https://bun.com/reference/node/inspector/Debugger/GetScriptSourceReturnType)>;

    Returns source for the script with given id.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setPauseOnExceptions',

    params?: [SetPauseOnExceptionsParameterType](https://bun.com/reference/node/inspector/Debugger/SetPauseOnExceptionsParameterType)

    ): Promise<void>;

    Defines pause on exceptions state. Can be set to stop on all exceptions, uncaught exceptions or no exceptions. Initial pause on exceptions state is <code>none</code>.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.evaluateOnCallFrame',

    params?: [EvaluateOnCallFrameParameterType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameParameterType)

    ): Promise<[EvaluateOnCallFrameReturnType](https://bun.com/reference/node/inspector/Debugger/EvaluateOnCallFrameReturnType)>;

    Evaluates expression on a given call frame.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setVariableValue',

    params?: [SetVariableValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetVariableValueParameterType)

    ): Promise<void>;

    Changes value of variable in a callframe. Object-based scopes are not supported and must be mutated manually.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setReturnValue',

    params?: [SetReturnValueParameterType](https://bun.com/reference/node/inspector/Debugger/SetReturnValueParameterType)

    ): Promise<void>;

    Changes return value in top frame. Available only at return break position.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setAsyncCallStackDepth',

    params?: [SetAsyncCallStackDepthParameterType](https://bun.com/reference/node/inspector/Debugger/SetAsyncCallStackDepthParameterType)

    ): Promise<void>;

    Enables or disables async call stacks tracking.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setBlackboxPatterns',

    params?: [SetBlackboxPatternsParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxPatternsParameterType)

    ): Promise<void>;

    Replace previous blackbox patterns with passed ones. Forces backend to skip stepping/pausing in scripts with url matching one of the patterns. VM will try to leave blackboxed script by performing 'step in' several times, finally resorting to 'step out' if unsuccessful.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Debugger.setBlackboxedRanges',

    params?: [SetBlackboxedRangesParameterType](https://bun.com/reference/node/inspector/Debugger/SetBlackboxedRangesParameterType)

    ): Promise<void>;

    Makes backend skip steps in the script in blackboxed ranges. VM will try leave blacklisted scripts by performing 'step in' several times, finally resorting to 'step out' if unsuccessful. Positions array contains positions where blackbox state is changed. First interval isn't blackboxed. Array should be sorted.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Console.enable'

    ): Promise<void>;

    Enables console domain, sends the messages collected so far to the client by means of the <code>messageAdded</code> notification.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Console.disable'

    ): Promise<void>;

    Disables console domain, prevents further console messages from being reported to the client.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Console.clearMessages'

    ): Promise<void>;

    Does nothing.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.enable'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.disable'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.setSamplingInterval',

    params?: [SetSamplingIntervalParameterType](https://bun.com/reference/node/inspector/Profiler/SetSamplingIntervalParameterType)

    ): Promise<void>;

    Changes CPU profiler sampling interval. Must be called before CPU profiles recording started.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.start'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.stop'

    ): Promise<[StopReturnType](https://bun.com/reference/node/inspector/Profiler/StopReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.startPreciseCoverage',

    params?: [StartPreciseCoverageParameterType](https://bun.com/reference/node/inspector/Profiler/StartPreciseCoverageParameterType)

    ): Promise<void>;

    Enable precise code coverage. Coverage data for JavaScript executed before enabling precise code coverage may be incomplete. Enabling prevents running optimized code and resets execution counters.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.stopPreciseCoverage'

    ): Promise<void>;

    Disable precise code coverage. Disabling releases unnecessary execution count records and allows executing optimized code.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.takePreciseCoverage'

    ): Promise<[TakePreciseCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/TakePreciseCoverageReturnType)>;

    Collect coverage data for the current isolate, and resets execution counters. Precise code coverage needs to have started.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Profiler.getBestEffortCoverage'

    ): Promise<[GetBestEffortCoverageReturnType](https://bun.com/reference/node/inspector/Profiler/GetBestEffortCoverageReturnType)>;

    Collect coverage data for the current isolate. The coverage data may be incomplete due to garbage collection.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.enable'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.disable'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.startTrackingHeapObjects',

    params?: [StartTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartTrackingHeapObjectsParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.stopTrackingHeapObjects',

    params?: [StopTrackingHeapObjectsParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StopTrackingHeapObjectsParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.takeHeapSnapshot',

    params?: [TakeHeapSnapshotParameterType](https://bun.com/reference/node/inspector/HeapProfiler/TakeHeapSnapshotParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.collectGarbage'

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.getObjectByHeapObjectId',

    params?: [GetObjectByHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdParameterType)

    ): Promise<[GetObjectByHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetObjectByHeapObjectIdReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.addInspectedHeapObject',

    params?: [AddInspectedHeapObjectParameterType](https://bun.com/reference/node/inspector/HeapProfiler/AddInspectedHeapObjectParameterType)

    ): Promise<void>;

    Enables console to refer to the node with given id via $x (see Command Line API for more details $x functions).

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.getHeapObjectId',

    params?: [GetHeapObjectIdParameterType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdParameterType)

    ): Promise<[GetHeapObjectIdReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetHeapObjectIdReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.startSampling',

    params?: [StartSamplingParameterType](https://bun.com/reference/node/inspector/HeapProfiler/StartSamplingParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.stopSampling'

    ): Promise<[StopSamplingReturnType](https://bun.com/reference/node/inspector/HeapProfiler/StopSamplingReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'HeapProfiler.getSamplingProfile'

    ): Promise<[GetSamplingProfileReturnType](https://bun.com/reference/node/inspector/HeapProfiler/GetSamplingProfileReturnType)>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeTracing.getCategories'

    ): Promise<[GetCategoriesReturnType](https://bun.com/reference/node/inspector/NodeTracing/GetCategoriesReturnType)>;

    Gets supported tracing categories.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeTracing.start',

    params?: [StartParameterType](https://bun.com/reference/node/inspector/NodeTracing/StartParameterType)

    ): Promise<void>;

    Start trace events collection.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeTracing.stop'

    ): Promise<void>;

    Stop trace events collection. Remaining collected events will be sent as a sequence of dataCollected events followed by tracingComplete event.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeWorker.sendMessageToWorker',

    params?: [SendMessageToWorkerParameterType](https://bun.com/reference/node/inspector/NodeWorker/SendMessageToWorkerParameterType)

    ): Promise<void>;

    Sends protocol message over session with given id.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeWorker.enable',

    params?: [EnableParameterType](https://bun.com/reference/node/inspector/NodeWorker/EnableParameterType)

    ): Promise<void>;

    Instructs the inspector to attach to running workers. Will also attach to new workers as they start

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeWorker.disable'

    ): Promise<void>;

    Detaches from all running workers and disables attaching to new workers as they are started.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeWorker.detach',

    params?: [DetachParameterType](https://bun.com/reference/node/inspector/NodeWorker/DetachParameterType)

    ): Promise<void>;

    Detached from the worker with given sessionId.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.disable'

    ): Promise<void>;

    Disables network tracking, prevents network events from being sent to the client.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.enable'

    ): Promise<void>;

    Enables network tracking, network events will now be delivered to the client.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.getRequestPostData',

    params?: [GetRequestPostDataParameterType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataParameterType)

    ): Promise<[GetRequestPostDataReturnType](https://bun.com/reference/node/inspector/Network/GetRequestPostDataReturnType)>;

    Returns post data sent with the request. Returns an error when no data was sent with the request.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.getResponseBody',

    params?: [GetResponseBodyParameterType](https://bun.com/reference/node/inspector/Network/GetResponseBodyParameterType)

    ): Promise<[GetResponseBodyReturnType](https://bun.com/reference/node/inspector/Network/GetResponseBodyReturnType)>;

    Returns content served for the given request.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.streamResourceContent',

    params?: [StreamResourceContentParameterType](https://bun.com/reference/node/inspector/Network/StreamResourceContentParameterType)

    ): Promise<[StreamResourceContentReturnType](https://bun.com/reference/node/inspector/Network/StreamResourceContentReturnType)>;

    Enables streaming of the response for the given requestId. If enabled, the dataReceived event contains the data that was received during streaming.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Network.loadNetworkResource',

    params?: [LoadNetworkResourceParameterType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceParameterType)

    ): Promise<[LoadNetworkResourceReturnType](https://bun.com/reference/node/inspector/Network/LoadNetworkResourceReturnType)>;

    Fetches the resource and returns the content.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeRuntime.enable'

    ): Promise<void>;

    Enable the NodeRuntime events except by `NodeRuntime.waitingForDisconnect`.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeRuntime.disable'

    ): Promise<void>;

    Disable NodeRuntime events

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'NodeRuntime.notifyWhenWaitingForDisconnect',

    params?: [NotifyWhenWaitingForDisconnectParameterType](https://bun.com/reference/node/inspector/NodeRuntime/NotifyWhenWaitingForDisconnectParameterType)

    ): Promise<void>;

    Enable the `NodeRuntime.waitingForDisconnect`.

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'Target.setAutoAttach',

    params?: [SetAutoAttachParameterType](https://bun.com/reference/node/inspector/Target/SetAutoAttachParameterType)

    ): Promise<void>;

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'IO.read',

    params?: [ReadParameterType](https://bun.com/reference/node/inspector/IO/ReadParameterType)

    ): Promise<[ReadReturnType](https://bun.com/reference/node/inspector/IO/ReadReturnType)>;

    Read a chunk of the stream

    [post](https://bun.com/reference/node/inspector/promises/Session/post)(

    method: 'IO.close',

    params?: [CloseParameterType](https://bun.com/reference/node/inspector/IO/CloseParameterType)

    ): Promise<void>;
  + [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

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

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/inspector/promises/Session/prependListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'inspectorNotification',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<object>) => void

    ): this;

    Emitted when any notification from the V8 Inspector is received.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.executionContextCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextCreatedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextCreatedEventDataType)>) => void

    ): this;

    Issued when new execution context is created.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.executionContextDestroyed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExecutionContextDestroyedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExecutionContextDestroyedEventDataType)>) => void

    ): this;

    Issued when execution context is destroyed.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.executionContextsCleared',

    listener: () => void

    ): this;

    Issued when all executionContexts were cleared in browser

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.exceptionThrown',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionThrownEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionThrownEventDataType)>) => void

    ): this;

    Issued when exception was thrown and unhandled.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.exceptionRevoked',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ExceptionRevokedEventDataType](https://bun.com/reference/node/inspector/Runtime/ExceptionRevokedEventDataType)>) => void

    ): this;

    Issued when unhandled exception was revoked.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.consoleAPICalled',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleAPICalledEventDataType](https://bun.com/reference/node/inspector/Runtime/ConsoleAPICalledEventDataType)>) => void

    ): this;

    Issued when console API was called.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Runtime.inspectRequested',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[InspectRequestedEventDataType](https://bun.com/reference/node/inspector/Runtime/InspectRequestedEventDataType)>) => void

    ): this;

    Issued when object should be inspected (for example, as a result of inspect() command line API call).

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Debugger.scriptParsed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptParsedEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptParsedEventDataType)>) => void

    ): this;

    Fired when virtual machine parses script. This event is also fired for all known and uncollected scripts upon enabling debugger.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Debugger.scriptFailedToParse',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ScriptFailedToParseEventDataType](https://bun.com/reference/node/inspector/Debugger/ScriptFailedToParseEventDataType)>) => void

    ): this;

    Fired when virtual machine fails to parse the script.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Debugger.breakpointResolved',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[BreakpointResolvedEventDataType](https://bun.com/reference/node/inspector/Debugger/BreakpointResolvedEventDataType)>) => void

    ): this;

    Fired when breakpoint is resolved to an actual script and location.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Debugger.paused',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[PausedEventDataType](https://bun.com/reference/node/inspector/Debugger/PausedEventDataType)>) => void

    ): this;

    Fired when the virtual machine stopped on breakpoint or exception or any other stop criteria.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Debugger.resumed',

    listener: () => void

    ): this;

    Fired when the virtual machine resumed execution.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Console.messageAdded',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[MessageAddedEventDataType](https://bun.com/reference/node/inspector/Console/MessageAddedEventDataType)>) => void

    ): this;

    Issued when new console message is added.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Profiler.consoleProfileStarted',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileStartedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileStartedEventDataType)>) => void

    ): this;

    Sent when new profile recording is started using console.profile() call.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Profiler.consoleProfileFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ConsoleProfileFinishedEventDataType](https://bun.com/reference/node/inspector/Profiler/ConsoleProfileFinishedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'HeapProfiler.addHeapSnapshotChunk',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AddHeapSnapshotChunkEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/AddHeapSnapshotChunkEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'HeapProfiler.resetProfiles',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'HeapProfiler.reportHeapSnapshotProgress',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReportHeapSnapshotProgressEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/ReportHeapSnapshotProgressEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'HeapProfiler.lastSeenObjectId',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LastSeenObjectIdEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/LastSeenObjectIdEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend regularly sends a current value for last seen object id and corresponding timestamp. If the were changes in the heap since last event then one or more heapStatsUpdate events will be sent before a new lastSeenObjectId event.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'HeapProfiler.heapStatsUpdate',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[HeapStatsUpdateEventDataType](https://bun.com/reference/node/inspector/HeapProfiler/HeapStatsUpdateEventDataType)>) => void

    ): this;

    If heap objects tracking has been started then backend may send update for one or more fragments

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeTracing.dataCollected',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataCollectedEventDataType](https://bun.com/reference/node/inspector/NodeTracing/DataCollectedEventDataType)>) => void

    ): this;

    Contains an bucket of collected trace events.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeTracing.tracingComplete',

    listener: () => void

    ): this;

    Signals that tracing is stopped and there is no trace buffers pending flush, all data were delivered via dataCollected events.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeWorker.attachedToWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/AttachedToWorkerEventDataType)>) => void

    ): this;

    Issued when attached to a worker.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeWorker.detachedFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DetachedFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/DetachedFromWorkerEventDataType)>) => void

    ): this;

    Issued when detached from the worker.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeWorker.receivedMessageFromWorker',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ReceivedMessageFromWorkerEventDataType](https://bun.com/reference/node/inspector/NodeWorker/ReceivedMessageFromWorkerEventDataType)>) => void

    ): this;

    Notifies about a new protocol message received from the session (session ID is provided in attachedToWorker notification).

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.requestWillBeSent',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[RequestWillBeSentEventDataType](https://bun.com/reference/node/inspector/Network/RequestWillBeSentEventDataType)>) => void

    ): this;

    Fired when page is about to send HTTP request.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.responseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[ResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/ResponseReceivedEventDataType)>) => void

    ): this;

    Fired when HTTP response is available.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.loadingFailed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFailedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFailedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.loadingFinished',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[LoadingFinishedEventDataType](https://bun.com/reference/node/inspector/Network/LoadingFinishedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.dataReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[DataReceivedEventDataType](https://bun.com/reference/node/inspector/Network/DataReceivedEventDataType)>) => void

    ): this;

    Fired when data chunk was received over the network.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.webSocketCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketCreatedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketCreatedEventDataType)>) => void

    ): this;

    Fired upon WebSocket creation.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.webSocketClosed',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketClosedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketClosedEventDataType)>) => void

    ): this;

    Fired when WebSocket is closed.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Network.webSocketHandshakeResponseReceived',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[WebSocketHandshakeResponseReceivedEventDataType](https://bun.com/reference/node/inspector/Network/WebSocketHandshakeResponseReceivedEventDataType)>) => void

    ): this;

    Fired when WebSocket handshake response becomes available.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeRuntime.waitingForDisconnect',

    listener: () => void

    ): this;

    This event is fired instead of `Runtime.executionContextDestroyed` when enabled. It is fired when the Node process finished all code execution and is waiting for all frontends to disconnect.

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'NodeRuntime.waitingForDebugger',

    listener: () => void

    ): this;

    This event is fired when the runtime is waiting for the debugger. For example, when inspector.waitingForDebugger is called

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Target.targetCreated',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[TargetCreatedEventDataType](https://bun.com/reference/node/inspector/Target/TargetCreatedEventDataType)>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/inspector/promises/Session/prependOnceListener)(

    event: 'Target.attachedToTarget',

    listener: (message: [InspectorNotification](https://bun.com/reference/node/inspector/InspectorNotification)<[AttachedToTargetEventDataType](https://bun.com/reference/node/inspector/Target/AttachedToTargetEventDataType)>) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/inspector/promises/Session/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/inspector/promises/Session/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/inspector/promises/Session/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/inspector/promises/Session/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/inspector/promises/Session/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/inspector/promises/Session/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/inspector/promises/Session/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/inspector/promises/Session/on)(

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

    static [on](https://bun.com/reference/node/inspector/promises/Session/on)(

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
  + static [once](https://bun.com/reference/node/inspector/promises/Session/once)(

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

    static [once](https://bun.com/reference/node/inspector/promises/Session/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/inspector/promises/Session/setMaxListeners)(

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