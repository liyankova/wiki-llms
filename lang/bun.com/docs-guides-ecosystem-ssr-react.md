---
url: https://bun.com/docs/guides/ecosystem/ssr-react
title: Server-side render (SSR) a React component - Bun
source_domain: bun.com
---

# Server-side render (SSR) a React component - Bun

To get started, install `react` & `react-dom`:

terminal

Copy

```
# Any package manager can be used
bun add react react-dom
```

---

To render a React component to an HTML stream server-side (SSR):

ssr-react.tsx

Copy

```
import { renderToReadableStream } from "react-dom/server";

function Component(props: { message: string }) {
  return (
    <body>
      <h1>{props.message}</h1>
    </body>
  );
}

const stream = await renderToReadableStream(<Component message="Hello from server!" />);
```

---

Combining this with `Bun.serve()`, we get a simple SSR HTTP server:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
Bun.serve({
  async fetch() {
    const stream = await renderToReadableStream(<Component message="Hello from server!" />);
    return new Response(stream, {
      headers: { "Content-Type": "text/html" },
    });
  },
});
```

---

React `19` and later includes an [SSR optimization](https://github.com/facebook/react/pull/25597) that takes advantage of Bun’s “direct” `ReadableStream` implementation. If you run into an error like `export named 'renderToReadableStream' not found`, please make sure to install version `19` of `react` & `react-dom`, or import from `react-dom/server.browser` instead of `react-dom/server`. See [facebook/react#28941](https://github.com/facebook/react/issues/28941) for more information.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/ssr-react.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/ssr-react)

⌘I