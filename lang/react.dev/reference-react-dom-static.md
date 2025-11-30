---
url: https://react.dev/reference/react-dom/static
title: Static React DOM APIs – React
source_domain: react.dev
---

# Static React DOM APIs – React

[API Reference](https://react.dev/reference/react)

# Static React DOM APIs

The `react-dom/static` APIs let you generate static HTML for React components. They have limited functionality compared to the streaming APIs. A [framework](https://react.dev/learn/creating-a-react-app#full-stack-frameworks) may call them for you. Most of your components don’t need to import or use them.

---

## Static APIs for Web Streams

These methods are only available in the environments with [Web Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), which includes browsers, Deno, and some modern edge runtimes:

* [`prerender`](https://react.dev/reference/react-dom/static/prerender) renders a React tree to static HTML with a [Readable Web Stream.](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)
* Experimental only [`resumeAndPrerender`](https://react.dev/reference/react-dom/static/resumeAndPrerender) continues a prerendered React tree to static HTML with a [Readable Web Stream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).

Node.js also includes these methods for compatibility, but they are not recommended due to worse performance. Use the [dedicated Node.js APIs](https://react.dev/reference/react-dom/static#static-apis-for-nodejs-streams) instead.

---

## Static APIs for Node.js Streams

These methods are only available in the environments with [Node.js Streams](https://nodejs.org/api/stream.html):

* [`prerenderToNodeStream`](https://react.dev/reference/react-dom/static/prerenderToNodeStream) renders a React tree to static HTML with a [Node.js Stream.](https://nodejs.org/api/stream.html)
* Experimental only [`resumeAndPrerenderToNodeStream`](https://react.dev/reference/react-dom/static/resumeAndPrerenderToNodeStream) continues a prerendered React tree to static HTML with a [Node.js Stream.](https://nodejs.org/api/stream.html)

[PreviousresumeToPipeableStream](https://react.dev/reference/react-dom/server/resumeToPipeableStream)[Nextprerender](https://react.dev/reference/react-dom/static/prerender)