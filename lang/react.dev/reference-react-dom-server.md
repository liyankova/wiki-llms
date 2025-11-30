---
url: https://react.dev/reference/react-dom/server
title: Server React DOM APIs – React
source_domain: react.dev
---

# Server React DOM APIs – React

[API Reference](https://react.dev/reference/react)

# Server React DOM APIs

The `react-dom/server` APIs let you server-side render React components to HTML. These APIs are only used on the server at the top level of your app to generate the initial HTML. A [framework](https://react.dev/learn/creating-a-react-app#full-stack-frameworks) may call them for you. Most of your components don’t need to import or use them.

---

## Server APIs for Web Streams

These methods are only available in the environments with [Web Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), which includes browsers, Deno, and some modern edge runtimes:

* [`renderToReadableStream`](https://react.dev/reference/react-dom/server/renderToReadableStream) renders a React tree to a [Readable Web Stream.](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)
* [`resume`](https://react.dev/reference/react-dom/server/renderToPipeableStream) resumes [`prerender`](https://react.dev/reference/react-dom/static/prerender) to a [Readable Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).

### Note

Node.js also includes these methods for compatibility, but they are not recommended due to worse performance. Use the [dedicated Node.js APIs](https://react.dev/reference/react-dom/server#server-apis-for-nodejs-streams) instead.

---

## Server APIs for Node.js Streams

These methods are only available in the environments with [Node.js Streams:](https://nodejs.org/api/stream.html)

* [`renderToPipeableStream`](https://react.dev/reference/react-dom/server/renderToPipeableStream) renders a React tree to a pipeable [Node.js Stream.](https://nodejs.org/api/stream.html)
* [`resumeToPipeableStream`](https://react.dev/reference/react-dom/server/renderToPipeableStream) resumes [`prerenderToNodeStream`](https://react.dev/reference/react-dom/static/prerenderToNodeStream) to a pipeable [Node.js Stream.](https://nodejs.org/api/stream.html)

---

## Legacy Server APIs for non-streaming environments

These methods can be used in the environments that don’t support streams:

* [`renderToString`](https://react.dev/reference/react-dom/server/renderToString) renders a React tree to a string.
* [`renderToStaticMarkup`](https://react.dev/reference/react-dom/server/renderToStaticMarkup) renders a non-interactive React tree to a string.

They have limited functionality compared to the streaming APIs.

[PrevioushydrateRoot](https://react.dev/reference/react-dom/client/hydrateRoot)[NextrenderToPipeableStream](https://react.dev/reference/react-dom/server/renderToPipeableStream)