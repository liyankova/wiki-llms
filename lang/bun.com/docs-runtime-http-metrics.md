---
url: https://bun.com/docs/runtime/http/metrics
title: Metrics - Bun
source_domain: bun.com
---

# Metrics - Bun

### [​](https://bun.com/docs/runtime/http/metrics#server-pendingrequests-and-server-pendingwebsockets) `server.pendingRequests` and `server.pendingWebSockets`

Monitor server activity with built-in counters:

Copy

```
const server = Bun.serve({
  fetch(req, server) {
    return new Response(
      `Active requests: ${server.pendingRequests}\n` + `Active WebSockets: ${server.pendingWebSockets}`,
    );
  },
});
```

### [​](https://bun.com/docs/runtime/http/metrics#server-subscribercount-topic) `server.subscriberCount(topic)`

Get count of subscribers for a WebSocket topic:

Copy

```
const server = Bun.serve({
  fetch(req, server) {
    const chatUsers = server.subscriberCount("chat");
    return new Response(`${chatUsers} users in chat`);
  },
  websocket: {
    message(ws) {
      ws.subscribe("chat");
    },
  },
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/http/metrics.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/http/metrics)

⌘I