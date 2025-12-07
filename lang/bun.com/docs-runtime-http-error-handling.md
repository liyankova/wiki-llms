---
url: https://bun.com/docs/runtime/http/error-handling
title: Error Handling - Bun
source_domain: bun.com
---

# Error Handling - Bun

To activate development mode, set `development: true`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
Bun.serve({
  development: true, 
  fetch(req) {
    throw new Error("woops!");
  },
});
```

In development mode, Bun will surface errors in-browser with a built-in error page.

![Bun's built-in 500 page](https://mintcdn.com/bun-1dd33a4e/PY1574V41bdK8wNs/images/exception_page.png?fit=max&auto=format&n=PY1574V41bdK8wNs&q=85&s=26f9bec162e97288f1f0d736773b2b6e)

### [​](https://bun.com/docs/runtime/http/error-handling#error-callback) `error` callback

To handle server-side errors, implement an `error` handler. This function should return a `Response` to serve to the client when an error occurs. This response will supersede Bun’s default error page in `development` mode.

Copy

```
Bun.serve({
  fetch(req) {
    throw new Error("woops!");
  },
  error(error) {
    return new Response(`<pre>${error}\n${error.stack}</pre>`, {
      headers: {
        "Content-Type": "text/html",
      },
    });
  },
});
```

[Learn more about debugging in Bun](https://bun.com/docs/runtime/debugger)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/http/error-handling.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/http/error-handling)

⌘I