---
url: https://bun.com/docs/runtime/networking/udp
title: UDP - Bun
source_domain: bun.com
---

# UDP - Bun

## [​](https://bun.com/docs/runtime/networking/udp#bind-a-udp-socket-bun-udpsocket) Bind a UDP socket (`Bun.udpSocket()`)

To create a new (bound) UDP socket:

Copy

```
const socket = await Bun.udpSocket({});
console.log(socket.port); // assigned by the operating system
```

Specify a port:

Copy

```
const socket = await Bun.udpSocket({
  port: 41234, 
});

console.log(socket.port); // 41234
```

### [​](https://bun.com/docs/runtime/networking/udp#send-a-datagram) Send a datagram

Specify the data to send, as well as the destination port and address.

Copy

```
socket.send("Hello, world!", 41234, "127.0.0.1");
```

Note that the address must be a valid IP address - `send` does not perform
DNS resolution, as it is intended for low-latency operations.

### [​](https://bun.com/docs/runtime/networking/udp#receive-datagrams) Receive datagrams

When creating your socket, add a callback to specify what should be done when packets are received:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const server = await Bun.udpSocket({
  socket: {
    data(socket, buf, port, addr) {
      console.log(`message from ${addr}:${port}:`);
      console.log(buf.toString());
    },
  },
});

const client = await Bun.udpSocket({});
client.send("Hello!", server.port, "127.0.0.1");
```

### [​](https://bun.com/docs/runtime/networking/udp#connections) Connections

While UDP does not have a concept of a connection, many UDP communications (especially as a client) involve only one peer.
In such cases it can be beneficial to connect the socket to that peer, which specifies to which address all packets are sent
and restricts incoming packets to that peer only.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const server = await Bun.udpSocket({
  socket: {
    data(socket, buf, port, addr) {
      console.log(`message from ${addr}:${port}:`);
      console.log(buf.toString());
    },
  },
});

const client = await Bun.udpSocket({
  connect: {
    port: server.port,
    hostname: "127.0.0.1",
  },
});

client.send("Hello");
```

Because connections are implemented on the operating system level, you can potentially observe performance benefits, too.

### [​](https://bun.com/docs/runtime/networking/udp#send-many-packets-at-once-using-sendmany) Send many packets at once using `sendMany()`

If you want to send a large volume of packets at once, it can make sense to batch them all together to avoid the overhead
of making a system call for each. This is made possible by the `sendMany()` API:
For an unconnected socket, `sendMany` takes an array as its only argument. Each set of three array elements describes a packet:
The first item is the data to be sent, the second is the target port, and the last is the target address.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const socket = await Bun.udpSocket({});

// sends 'Hello' to 127.0.0.1:41234, and 'foo' to 1.1.1.1:53 in a single operation
socket.sendMany(["Hello", 41234, "127.0.0.1", "foo", 53, "1.1.1.1"]);
```

With a connected socket, `sendMany` simply takes an array, where each element represents the data to be sent to the peer.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const socket = await Bun.udpSocket({
  connect: {
    port: 41234,
    hostname: "localhost",
  },
});

socket.sendMany(["foo", "bar", "baz"]);
```

`sendMany` returns the number of packets that were successfully sent. As with `send`, `sendMany` only takes valid IP addresses
as destinations, as it does not perform DNS resolution.

### [​](https://bun.com/docs/runtime/networking/udp#handle-backpressure) Handle backpressure

It may happen that a packet that you’re sending does not fit into the operating system’s packet buffer. You can detect that this
has happened when:

* `send` returns `false`
* `sendMany` returns a number smaller than the number of packets you specified. In this case, the `drain` socket handler will be called once the socket becomes writable again:

Copy

```
const socket = await Bun.udpSocket({
  socket: {
    drain(socket) {
      // continue sending data
    },
  },
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/networking/udp.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/networking/udp)

⌘I