---
url: https://bun.com/docs/guides/http/proxy
title: Proxy HTTP requests using fetch() - Bun
source_domain: bun.com
---

# Proxy HTTP requests using fetch() - Bun

In Bun, `fetch` supports sending requests through an HTTP or HTTPS proxy. This is useful on corporate networks or when you need to ensure a request is sent through a specific IP address.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)proxy.ts

Copy

```
await fetch("https://example.com", {
  // The URL of the proxy server
  proxy: "https://username:[email protected]:8080",
});
```

---

The `proxy` option can be a URL string or an object with `url` and optional `headers`. The URL can include the username and password if the proxy requires authentication. It can be `http://` or `https://`.

---

## [​](https://bun.com/docs/guides/http/proxy#custom-proxy-headers) Custom proxy headers

To send custom headers to the proxy server (useful for proxy authentication tokens, custom routing, etc.), use the object format:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)proxy-headers.ts

Copy

```
await fetch("https://example.com", {
  proxy: {
    url: "https://proxy.example.com:8080",
    headers: {
      "Proxy-Authorization": "Bearer my-token",
      "X-Proxy-Region": "us-east-1",
    },
  },
});
```

The `headers` property accepts a plain object or a `Headers` instance. These headers are sent directly to the proxy server in `CONNECT` requests (for HTTPS targets) or in the proxy request (for HTTP targets).
If you provide a `Proxy-Authorization` header, it will override any credentials specified in the proxy URL.

---

## [​](https://bun.com/docs/guides/http/proxy#environment-variables) Environment variables

You can also set the `$HTTP_PROXY` or `$HTTPS_PROXY` environment variable to the proxy URL. This is useful when you want to use the same proxy for all requests.

terminal

Copy

```
HTTPS_PROXY=https://username:[email protected]:8080 bun run index.ts
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/proxy.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/proxy)

⌘I