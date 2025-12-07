---
url: https://bun.com/docs/guides/http/fetch-unix
title: fetch with unix domain sockets in Bun - Bun
source_domain: bun.com
---

# fetch with unix domain sockets in Bun - Bun

In Bun, the `unix` option in `fetch()` lets you send HTTP requests over a [unix domain socket](https://en.wikipedia.org/wiki/Unix_domain_socket).

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)fetch-unix.ts

Copy

```
const unix = "/var/run/docker.sock";

const response = await fetch("http://localhost/info", { unix });

const body = await response.json();
console.log(body); // { ... }
```

---

The `unix` option is a string that specifies the local file path to a unix domain socket. The `fetch()` function will use the socket to send the request to the server instead of using a TCP network connection. `https` is also supported by using the `https://` protocol in the URL instead of `http://`.
To send a `POST` request to an API endpoint over a unix domain socket:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)fetch-unix.ts

Copy

```
const response = await fetch("https://hostname/a/path", {
  unix: "/var/run/path/to/unix.sock",
  method: "POST",
  body: JSON.stringify({ message: "Hello from Bun!" }),
  headers: {
    "Content-Type": "application/json",
  },
});

const body = await response.json();
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/fetch-unix.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/fetch-unix)

⌘I