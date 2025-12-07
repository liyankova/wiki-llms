---
url: https://bun.com/reference/node/dns
title: Node.js dns module | API Reference | Bun
source_domain: bun.com
---

# Node.js dns module | API Reference | Bun

Node.js module

# [dns](https://bun.com/reference/node/dns)

The `'node:dns'` module provides DNS lookup and resolution services. It supports synchronous and asynchronous methods to resolve host names, addresses, and service records.

Functions include `lookup`, `resolve`, `reverse`, and others for fetching various DNS record types like A, AAAA, CNAME, MX, PTR, SRV, and TXT.

Works in Bun

Fully implemented. > 90% of Node.js's test suite passes.

* ### class [Resolver](https://bun.com/reference/node/dns/Resolver)

  An independent resolver for DNS requests.

  Creating a new resolver uses the default server settings. Setting the servers used for a resolver using [`resolver.setServers()`](https://nodejs.org/docs/latest-v24.x/api/dns.html#dnssetserversservers) does not affect other resolvers:

  ```
  import { Resolver } from 'node:dns';
  const resolver = new Resolver();
  resolver.setServers(['4.4.4.4']);

  // This request will use the server at 4.4.4.4, independent of global settings.
  resolver.resolve4('example.org', (err, addresses) => {
    // ...
  });
  ```

  The following methods from the `node:dns` module are available:

  + `resolver.getServers()`
  + `resolver.resolve()`
  + `resolver.resolve4()`
  + `resolver.resolve6()`
  + `resolver.resolveAny()`
  + `resolver.resolveCaa()`
  + `resolver.resolveCname()`
  + `resolver.resolveMx()`
  + `resolver.resolveNaptr()`
  + `resolver.resolveNs()`
  + `resolver.resolvePtr()`
  + `resolver.resolveSoa()`
  + `resolver.resolveSrv()`
  + `resolver.resolveTxt()`
  + `resolver.reverse()`
  + `resolver.setServers()`

  + [getServers](https://bun.com/reference/node/dns/Resolver/getServers): () => string[]
  + [resolve](https://bun.com/reference/node/dns/Resolver/resolve): typeof [resolve](https://bun.com/reference/node/dns/resolve)
  + [resolve4](https://bun.com/reference/node/dns/Resolver/resolve4): typeof [resolve4](https://bun.com/reference/node/dns/resolve4)
  + [resolve6](https://bun.com/reference/node/dns/Resolver/resolve6): typeof [resolve6](https://bun.com/reference/node/dns/resolve6)
  + [resolveAny](https://bun.com/reference/node/dns/Resolver/resolveAny): typeof [resolveAny](https://bun.com/reference/node/dns/resolveAny)
  + [resolveCaa](https://bun.com/reference/node/dns/Resolver/resolveCaa): typeof [resolveCaa](https://bun.com/reference/node/dns/resolveCaa)
  + [resolveCname](https://bun.com/reference/node/dns/Resolver/resolveCname): typeof [resolveCname](https://bun.com/reference/node/dns/resolveCname)
  + [resolveMx](https://bun.com/reference/node/dns/Resolver/resolveMx): typeof [resolveMx](https://bun.com/reference/node/dns/resolveMx)
  + [resolveNaptr](https://bun.com/reference/node/dns/Resolver/resolveNaptr): typeof [resolveNaptr](https://bun.com/reference/node/dns/resolveNaptr)
  + [resolveNs](https://bun.com/reference/node/dns/Resolver/resolveNs): typeof [resolveNs](https://bun.com/reference/node/dns/resolveNs)
  + [resolvePtr](https://bun.com/reference/node/dns/Resolver/resolvePtr): typeof [resolvePtr](https://bun.com/reference/node/dns/resolvePtr)
  + [resolveSoa](https://bun.com/reference/node/dns/Resolver/resolveSoa): typeof [resolveSoa](https://bun.com/reference/node/dns/resolveSoa)
  + [resolveSrv](https://bun.com/reference/node/dns/Resolver/resolveSrv): typeof [resolveSrv](https://bun.com/reference/node/dns/resolveSrv)
  + [resolveTlsa](https://bun.com/reference/node/dns/Resolver/resolveTlsa): typeof [resolveTlsa](https://bun.com/reference/node/dns/resolveTlsa)
  + [resolveTxt](https://bun.com/reference/node/dns/Resolver/resolveTxt): typeof [resolveTxt](https://bun.com/reference/node/dns/resolveTxt)
  + [reverse](https://bun.com/reference/node/dns/Resolver/reverse): (ip: string, callback: (err: null | ErrnoException, hostnames: string[]) => void) => void
  + [setServers](https://bun.com/reference/node/dns/Resolver/setServers): (servers: readonly string[]) => void
  + [cancel](https://bun.com/reference/node/dns/Resolver/cancel)(): void;

    Cancel all outstanding DNS queries made by this resolver. The corresponding callbacks will be called with an error with code `ECANCELLED`.
  + [setLocalAddress](https://bun.com/reference/node/dns/Resolver/setLocalAddress)(

    ipv4?: string,

    ipv6?: string

    ): void;

    The resolver instance will send its requests from the specified IP address. This allows programs to specify outbound interfaces when used on multi-homed systems.

    If a v4 or v6 address is not specified, it is set to the default and the operating system will choose a local address automatically.

    The resolver will use the v4 local address when making requests to IPv4 DNS servers, and the v6 local address when making requests to IPv6 DNS servers. The `rrtype` of resolution requests has no impact on the local address used.

    @param ipv4

    A string representation of an IPv4 address.

    @param ipv6

    A string representation of an IPv6 address.
* const [ADDRCONFIG](https://bun.com/reference/node/dns/ADDRCONFIG): number

  Limits returned address types to the types of non-loopback addresses configured on the system. For example, IPv4 addresses are only returned if the current system has at least one IPv4 address configured.
* const [ADDRGETNETWORKPARAMS](https://bun.com/reference/node/dns/ADDRGETNETWORKPARAMS): 'EADDRGETNETWORKPARAMS'
* const [ALL](https://bun.com/reference/node/dns/ALL): number

  If `dns.V4MAPPED` is specified, return resolved IPv6 addresses as well as IPv4 mapped IPv6 addresses.
* const [BADFAMILY](https://bun.com/reference/node/dns/BADFAMILY): 'EBADFAMILY'
* const [BADFLAGS](https://bun.com/reference/node/dns/BADFLAGS): 'EBADFLAGS'
* const [BADHINTS](https://bun.com/reference/node/dns/BADHINTS): 'EBADHINTS'
* const [BADNAME](https://bun.com/reference/node/dns/BADNAME): 'EBADNAME'
* const [BADQUERY](https://bun.com/reference/node/dns/BADQUERY): 'EBADQUERY'
* const [BADRESP](https://bun.com/reference/node/dns/BADRESP): 'EBADRESP'
* const [BADSTR](https://bun.com/reference/node/dns/BADSTR): 'EBADSTR'
* const [CANCELLED](https://bun.com/reference/node/dns/CANCELLED): 'ECANCELLED'
* const [CONNREFUSED](https://bun.com/reference/node/dns/CONNREFUSED): 'ECONNREFUSED'
* const [DESTRUCTION](https://bun.com/reference/node/dns/DESTRUCTION): 'EDESTRUCTION'
* const [EOF](https://bun.com/reference/node/dns/EOF): 'EOF'
* const [FILE](https://bun.com/reference/node/dns/FILE): 'EFILE'
* const [FORMERR](https://bun.com/reference/node/dns/FORMERR): 'EFORMERR'
* const [LOADIPHLPAPI](https://bun.com/reference/node/dns/LOADIPHLPAPI): 'ELOADIPHLPAPI'
* const [NODATA](https://bun.com/reference/node/dns/NODATA): 'ENODATA'
* const [NOMEM](https://bun.com/reference/node/dns/NOMEM): 'ENOMEM'
* const [NONAME](https://bun.com/reference/node/dns/NONAME): 'ENONAME'
* const [NOTFOUND](https://bun.com/reference/node/dns/NOTFOUND): 'ENOTFOUND'
* const [NOTIMP](https://bun.com/reference/node/dns/NOTIMP): 'ENOTIMP'
* const [NOTINITIALIZED](https://bun.com/reference/node/dns/NOTINITIALIZED): 'ENOTINITIALIZED'
* const [REFUSED](https://bun.com/reference/node/dns/REFUSED): 'EREFUSED'
* const [SERVFAIL](https://bun.com/reference/node/dns/SERVFAIL): 'ESERVFAIL'
* const [TIMEOUT](https://bun.com/reference/node/dns/TIMEOUT): 'ETIMEOUT'
* const [V4MAPPED](https://bun.com/reference/node/dns/V4MAPPED): number

  If the IPv6 family was specified, but no IPv6 addresses were found, then return IPv4 mapped IPv6 addresses. It is not supported on some operating systems (e.g. FreeBSD 10.1).
* function [getDefaultResultOrder](https://bun.com/reference/node/dns/getDefaultResultOrder)(): 'ipv4first' | 'ipv6first' | 'verbatim';

  Get the default value for `order` in lookup and [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v24.x/api/dns.html#dnspromiseslookuphostname-options). The value could be:

  + `ipv4first`: for `order` defaulting to `ipv4first`.
  + `ipv6first`: for `order` defaulting to `ipv6first`.
  + `verbatim`: for `order` defaulting to `verbatim`.
* function [getServers](https://bun.com/reference/node/dns/getServers)(): string[];

  Returns an array of IP address strings, formatted according to [RFC 5952](https://tools.ietf.org/html/rfc5952#section-6), that are currently configured for DNS resolution. A string will include a port section if a custom port is used.

  ```
  [
    '4.4.4.4',
    '2001:4860:4860::8888',
    '4.4.4.4:1053',
    '[2001:4860:4860::8888]:1053',
  ]
  ```
* function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  family: number,

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupOneOptions](https://bun.com/reference/node/dns/LookupOneOptions),

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupAllOptions](https://bun.com/reference/node/dns/LookupAllOptions),

  callback: (err: null | ErrnoException, addresses: [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[]) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupOptions](https://bun.com/reference/node/dns/LookupOptions),

  callback: (err: null | ErrnoException, address: string | [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[], family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.
* function [lookupService](https://bun.com/reference/node/dns/lookupService)(

  address: string,

  port: number,

  callback: (err: null | ErrnoException, hostname: string, service: string) => void

  ): void;

  Resolves the given `address` and `port` into a host name and service using the operating system's underlying `getnameinfo` implementation.

  If `address` is not a valid IP address, a `TypeError` will be thrown. The `port` will be coerced to a number. If it is not a legal port, a `TypeError` will be thrown.

  On an error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is the error code.

  ```
  import dns from 'node:dns';
  dns.lookupService('127.0.0.1', 22, (err, hostname, service) => {
    console.log(hostname, service);
    // Prints: localhost ssh
  });
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, it returns a `Promise` for an `Object` with `hostname` and `service` properties.
* function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'A' | 'AAAA' | 'CNAME' | 'NS' | 'PTR',

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'ANY',

  callback: (err: null | ErrnoException, addresses: [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'CAA',

  callback: (err: null | ErrnoException, address: [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'MX',

  callback: (err: null | ErrnoException, addresses: [MxRecord](https://bun.com/reference/node/dns/MxRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'NAPTR',

  callback: (err: null | ErrnoException, addresses: [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'SOA',

  callback: (err: null | ErrnoException, addresses: [SoaRecord](https://bun.com/reference/node/dns/SoaRecord)) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'SRV',

  callback: (err: null | ErrnoException, addresses: [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'TLSA',

  callback: (err: null | ErrnoException, addresses: [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'TXT',

  callback: (err: null | ErrnoException, addresses: string[][]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: string,

  callback: (err: null | ErrnoException, addresses: string[] | [SoaRecord](https://bun.com/reference/node/dns/SoaRecord) | [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[] | [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[] | [MxRecord](https://bun.com/reference/node/dns/MxRecord)[] | [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[] | [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[] | [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[] | string[][]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.
* function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions),

  callback: (err: null | ErrnoException, addresses: [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions),

  callback: (err: null | ErrnoException, addresses: string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.
* function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions),

  callback: (err: null | ErrnoException, addresses: [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions),

  callback: (err: null | ErrnoException, addresses: string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.
* function [resolveAny](https://bun.com/reference/node/dns/resolveAny)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve all records (also known as `ANY` or `*` query). The `ret` argument passed to the `callback` function will be an array containing various types of records. Each object has a property `type` that indicates the type of the current record. And depending on the `type`, additional properties will be present on the object:

  <omitted>

  Here is an example of the `ret` object passed to the callback:

  ```
  [ { type: 'A', address: '127.0.0.1', ttl: 299 },
    { type: 'CNAME', value: 'example.com' },
    { type: 'MX', exchange: 'alt4.aspmx.l.example.com', priority: 50 },
    { type: 'NS', value: 'ns1.example.com' },
    { type: 'TXT', entries: [ 'v=spf1 include:_spf.example.com ~all' ] },
    { type: 'SOA',
      nsname: 'ns1.example.com',
      hostmaster: 'admin.example.com',
      serial: 156696742,
      refresh: 900,
      retry: 900,
      expire: 1800,
      minttl: 60 } ]
  ```

  DNS server operators may choose not to respond to `ANY` queries. It may be better to call individual methods like resolve4, resolveMx, and so on. For more details, see [RFC 8482](https://tools.ietf.org/html/rfc8482).
* function [resolveCaa](https://bun.com/reference/node/dns/resolveCaa)(

  hostname: string,

  callback: (err: null | ErrnoException, records: [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve `CAA` records for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of certification authority authorization records available for the `hostname` (e.g. `[{critical: 0, iodef: 'mailto:pki@example.com'}, {critical: 128, issue: 'pki.example.com'}]`).
* function [resolveCname](https://bun.com/reference/node/dns/resolveCname)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve `CNAME` records for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of canonical name records available for the `hostname` (e.g. `['bar.example.com']`).
* function [resolveMx](https://bun.com/reference/node/dns/resolveMx)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [MxRecord](https://bun.com/reference/node/dns/MxRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve mail exchange records (`MX` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of objects containing both a `priority` and `exchange` property (e.g. `[{priority: 10, exchange: 'mx.example.com'}, ...]`).
* function [resolveNaptr](https://bun.com/reference/node/dns/resolveNaptr)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve regular expression-based records (`NAPTR` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of objects with the following properties:

  + `flags`
  + `service`
  + `regexp`
  + `replacement`
  + `order`
  + `preference`

  ```
  {
    flags: 's',
    service: 'SIP+D2U',
    regexp: '',
    replacement: '_sip._udp.example.com',
    order: 30,
    preference: 100
  }
  ```
* function [resolveNs](https://bun.com/reference/node/dns/resolveNs)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve name server records (`NS` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of name server records available for `hostname` (e.g. `['ns1.example.com', 'ns2.example.com']`).
* function [resolvePtr](https://bun.com/reference/node/dns/resolvePtr)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve pointer records (`PTR` records) for the `hostname`. The `addresses` argument passed to the `callback` function will be an array of strings containing the reply records.
* function [resolveSoa](https://bun.com/reference/node/dns/resolveSoa)(

  hostname: string,

  callback: (err: null | ErrnoException, address: [SoaRecord](https://bun.com/reference/node/dns/SoaRecord)) => void

  ): void;

  Uses the DNS protocol to resolve a start of authority record (`SOA` record) for the `hostname`. The `address` argument passed to the `callback` function will be an object with the following properties:

  + `nsname`
  + `hostmaster`
  + `serial`
  + `refresh`
  + `retry`
  + `expire`
  + `minttl`

  ```
  {
    nsname: 'ns.example.com',
    hostmaster: 'root.example.com',
    serial: 2013101809,
    refresh: 10000,
    retry: 2400,
    expire: 604800,
    minttl: 3600
  }
  ```
* function [resolveSrv](https://bun.com/reference/node/dns/resolveSrv)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve service records (`SRV` records) for the `hostname`. The `addresses` argument passed to the `callback` function will be an array of objects with the following properties:

  + `priority`
  + `weight`
  + `port`
  + `name`

  ```
  {
    priority: 10,
    weight: 5,
    port: 21223,
    name: 'service.example.com'
  }
  ```
* function [resolveTlsa](https://bun.com/reference/node/dns/resolveTlsa)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve certificate associations (`TLSA` records) for the `hostname`. The `records` argument passed to the `callback` function is an array of objects with these properties:

  + `certUsage`
  + `selector`
  + `match`
  + `data`

  ```
  {
    certUsage: 3,
    selector: 1,
    match: 1,
    data: [ArrayBuffer]
  }
  ```
* function [resolveTxt](https://bun.com/reference/node/dns/resolveTxt)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[][]) => void

  ): void;

  Uses the DNS protocol to resolve text queries (`TXT` records) for the `hostname`. The `records` argument passed to the `callback` function is a two-dimensional array of the text records available for `hostname` (e.g.`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`). Each sub-array contains TXT chunks of one record. Depending on the use case, these could be either joined together or treated separately.
* function [reverse](https://bun.com/reference/node/dns/reverse)(

  ip: string,

  callback: (err: null | ErrnoException, hostnames: string[]) => void

  ): void;

  Performs a reverse DNS query that resolves an IPv4 or IPv6 address to an array of host names.

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v24.x/api/dns.html#error-codes).
* function [setDefaultResultOrder](https://bun.com/reference/node/dns/setDefaultResultOrder)(

  order: 'ipv4first' | 'ipv6first' | 'verbatim'

  ): void;

  Set the default value of `order` in lookup and [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v24.x/api/dns.html#dnspromiseslookuphostname-options). The value could be:

  + `ipv4first`: sets default `order` to `ipv4first`.
  + `ipv6first`: sets default `order` to `ipv6first`.
  + `verbatim`: sets default `order` to `verbatim`.

  The default is `verbatim` and setDefaultResultOrder have higher priority than [`--dns-result-order`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--dns-result-orderorder). When using [worker threads](https://nodejs.org/docs/latest-v24.x/api/worker_threads.html), setDefaultResultOrder from the main thread won't affect the default dns orders in workers.

  @param order

  must be `'ipv4first'`, `'ipv6first'` or `'verbatim'`.
* function [setServers](https://bun.com/reference/node/dns/setServers)(

  servers: readonly string[]

  ): void;

  Sets the IP address and port of servers to be used when performing DNS resolution. The `servers` argument is an array of [RFC 5952](https://tools.ietf.org/html/rfc5952#section-6) formatted addresses. If the port is the IANA default DNS port (53) it can be omitted.

  ```
  dns.setServers([
    '4.4.4.4',
    '[2001:4860:4860::8888]',
    '4.4.4.4:1053',
    '[2001:4860:4860::8888]:1053',
  ]);
  ```

  An error will be thrown if an invalid address is provided.

  The `dns.setServers()` method must not be called while a DNS query is in progress.

  The setServers method affects only resolve, `dns.resolve*()` and reverse (and specifically *not* lookup).

  This method works much like [resolve.conf](https://man7.org/linux/man-pages/man5/resolv.conf.5.html). That is, if attempting to resolve with the first server provided results in a `NOTFOUND` error, the `resolve()` method will *not* attempt to resolve with subsequent servers provided. Fallback DNS servers will only be used if the earlier ones time out or result in some other error.

  @param servers

  array of [RFC 5952](https://datatracker.ietf.org/doc/html/rfc5952#section-6) formatted addresses

## Type definitions

* function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  family: number,

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupOneOptions](https://bun.com/reference/node/dns/LookupOneOptions),

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupAllOptions](https://bun.com/reference/node/dns/LookupAllOptions),

  callback: (err: null | ErrnoException, addresses: [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[]) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  options: [LookupOptions](https://bun.com/reference/node/dns/LookupOptions),

  callback: (err: null | ErrnoException, address: string | [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[], family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  function [lookup](https://bun.com/reference/node/dns/lookup)(

  hostname: string,

  callback: (err: null | ErrnoException, address: string, family: number) => void

  ): void;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is `0` or not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the arguments for `callback` change to `(err, addresses)`, with `addresses` being an array of objects with the properties `address` and `family`.

  On error, `err` is an `Error` object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  `dns.lookup()` does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v24.x/api/dns.html#implementation-considerations) before using `dns.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };
  dns.lookup('example.com', options, (err, address, family) =>
    console.log('address: %j family: IPv%s', address, family));
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

  // When options.all is true, the result will be an Array.
  options.all = true;
  dns.lookup('example.com', options, (err, addresses) =>
    console.log('addresses: %j', addresses));
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, and `all` is not set to `true`, it returns a `Promise` for an `Object` with `address` and `family` properties.

  ### namespace [lookup](https://bun.com/reference/node/dns/lookup)
* function [lookupService](https://bun.com/reference/node/dns/lookupService)(

  address: string,

  port: number,

  callback: (err: null | ErrnoException, hostname: string, service: string) => void

  ): void;

  Resolves the given `address` and `port` into a host name and service using the operating system's underlying `getnameinfo` implementation.

  If `address` is not a valid IP address, a `TypeError` will be thrown. The `port` will be coerced to a number. If it is not a legal port, a `TypeError` will be thrown.

  On an error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is the error code.

  ```
  import dns from 'node:dns';
  dns.lookupService('127.0.0.1', 22, (err, hostname, service) => {
    console.log(hostname, service);
    // Prints: localhost ssh
  });
  ```

  If this method is invoked as its [util.promisify()](https://nodejs.org/docs/latest-v24.x/api/util.html#utilpromisifyoriginal) ed version, it returns a `Promise` for an `Object` with `hostname` and `service` properties.

  ### namespace [lookupService](https://bun.com/reference/node/dns/lookupService)
* function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'A' | 'AAAA' | 'CNAME' | 'NS' | 'PTR',

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'ANY',

  callback: (err: null | ErrnoException, addresses: [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'CAA',

  callback: (err: null | ErrnoException, address: [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'MX',

  callback: (err: null | ErrnoException, addresses: [MxRecord](https://bun.com/reference/node/dns/MxRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'NAPTR',

  callback: (err: null | ErrnoException, addresses: [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'SOA',

  callback: (err: null | ErrnoException, addresses: [SoaRecord](https://bun.com/reference/node/dns/SoaRecord)) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'SRV',

  callback: (err: null | ErrnoException, addresses: [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'TLSA',

  callback: (err: null | ErrnoException, addresses: [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: 'TXT',

  callback: (err: null | ErrnoException, addresses: string[][]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/resolve)(

  hostname: string,

  rrtype: string,

  callback: (err: null | ErrnoException, addresses: string[] | [SoaRecord](https://bun.com/reference/node/dns/SoaRecord) | [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[] | [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[] | [MxRecord](https://bun.com/reference/node/dns/MxRecord)[] | [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[] | [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[] | [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[] | string[][]) => void

  ): void;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. The `callback` function has arguments `(err, records)`. When successful, `records` will be an array of resource records. The type and structure of individual results varies based on `rrtype`:

  <omitted>

  On error, `err` is an [`Error`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-error) object, where `err.code` is one of the `DNS error codes`.

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  ### namespace [resolve](https://bun.com/reference/node/dns/resolve)
* function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions),

  callback: (err: null | ErrnoException, addresses: [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/resolve4)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions),

  callback: (err: null | ErrnoException, addresses: string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve a IPv4 addresses (`A` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv4 addresses (e.g.`['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  ### namespace [resolve4](https://bun.com/reference/node/dns/resolve4)
* function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions),

  callback: (err: null | ErrnoException, addresses: [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/resolve6)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions),

  callback: (err: null | ErrnoException, addresses: string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]) => void

  ): void;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  ### namespace [resolve6](https://bun.com/reference/node/dns/resolve6)
* function [resolveAny](https://bun.com/reference/node/dns/resolveAny)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve all records (also known as `ANY` or `*` query). The `ret` argument passed to the `callback` function will be an array containing various types of records. Each object has a property `type` that indicates the type of the current record. And depending on the `type`, additional properties will be present on the object:

  <omitted>

  Here is an example of the `ret` object passed to the callback:

  ```
  [ { type: 'A', address: '127.0.0.1', ttl: 299 },
    { type: 'CNAME', value: 'example.com' },
    { type: 'MX', exchange: 'alt4.aspmx.l.example.com', priority: 50 },
    { type: 'NS', value: 'ns1.example.com' },
    { type: 'TXT', entries: [ 'v=spf1 include:_spf.example.com ~all' ] },
    { type: 'SOA',
      nsname: 'ns1.example.com',
      hostmaster: 'admin.example.com',
      serial: 156696742,
      refresh: 900,
      retry: 900,
      expire: 1800,
      minttl: 60 } ]
  ```

  DNS server operators may choose not to respond to `ANY` queries. It may be better to call individual methods like resolve4, resolveMx, and so on. For more details, see [RFC 8482](https://tools.ietf.org/html/rfc8482).

  ### namespace [resolveAny](https://bun.com/reference/node/dns/resolveAny)
* function [resolveCaa](https://bun.com/reference/node/dns/resolveCaa)(

  hostname: string,

  callback: (err: null | ErrnoException, records: [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve `CAA` records for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of certification authority authorization records available for the `hostname` (e.g. `[{critical: 0, iodef: 'mailto:pki@example.com'}, {critical: 128, issue: 'pki.example.com'}]`).

  ### namespace [resolveCaa](https://bun.com/reference/node/dns/resolveCaa)
* function [resolveCname](https://bun.com/reference/node/dns/resolveCname)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve `CNAME` records for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of canonical name records available for the `hostname` (e.g. `['bar.example.com']`).

  ### namespace [resolveCname](https://bun.com/reference/node/dns/resolveCname)
* function [resolveMx](https://bun.com/reference/node/dns/resolveMx)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [MxRecord](https://bun.com/reference/node/dns/MxRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve mail exchange records (`MX` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of objects containing both a `priority` and `exchange` property (e.g. `[{priority: 10, exchange: 'mx.example.com'}, ...]`).

  ### namespace [resolveMx](https://bun.com/reference/node/dns/resolveMx)
* function [resolveNaptr](https://bun.com/reference/node/dns/resolveNaptr)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve regular expression-based records (`NAPTR` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of objects with the following properties:

  + `flags`
  + `service`
  + `regexp`
  + `replacement`
  + `order`
  + `preference`

  ```
  {
    flags: 's',
    service: 'SIP+D2U',
    regexp: '',
    replacement: '_sip._udp.example.com',
    order: 30,
    preference: 100
  }
  ```

  ### namespace [resolveNaptr](https://bun.com/reference/node/dns/resolveNaptr)
* function [resolveNs](https://bun.com/reference/node/dns/resolveNs)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve name server records (`NS` records) for the `hostname`. The `addresses` argument passed to the `callback` function will contain an array of name server records available for `hostname` (e.g. `['ns1.example.com', 'ns2.example.com']`).

  ### namespace [resolveNs](https://bun.com/reference/node/dns/resolveNs)
* function [resolvePtr](https://bun.com/reference/node/dns/resolvePtr)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[]) => void

  ): void;

  Uses the DNS protocol to resolve pointer records (`PTR` records) for the `hostname`. The `addresses` argument passed to the `callback` function will be an array of strings containing the reply records.

  ### namespace [resolvePtr](https://bun.com/reference/node/dns/resolvePtr)
* function [resolveSoa](https://bun.com/reference/node/dns/resolveSoa)(

  hostname: string,

  callback: (err: null | ErrnoException, address: [SoaRecord](https://bun.com/reference/node/dns/SoaRecord)) => void

  ): void;

  Uses the DNS protocol to resolve a start of authority record (`SOA` record) for the `hostname`. The `address` argument passed to the `callback` function will be an object with the following properties:

  + `nsname`
  + `hostmaster`
  + `serial`
  + `refresh`
  + `retry`
  + `expire`
  + `minttl`

  ```
  {
    nsname: 'ns.example.com',
    hostmaster: 'root.example.com',
    serial: 2013101809,
    refresh: 10000,
    retry: 2400,
    expire: 604800,
    minttl: 3600
  }
  ```

  ### namespace [resolveSoa](https://bun.com/reference/node/dns/resolveSoa)
* function [resolveSrv](https://bun.com/reference/node/dns/resolveSrv)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve service records (`SRV` records) for the `hostname`. The `addresses` argument passed to the `callback` function will be an array of objects with the following properties:

  + `priority`
  + `weight`
  + `port`
  + `name`

  ```
  {
    priority: 10,
    weight: 5,
    port: 21223,
    name: 'service.example.com'
  }
  ```

  ### namespace [resolveSrv](https://bun.com/reference/node/dns/resolveSrv)
* function [resolveTlsa](https://bun.com/reference/node/dns/resolveTlsa)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]) => void

  ): void;

  Uses the DNS protocol to resolve certificate associations (`TLSA` records) for the `hostname`. The `records` argument passed to the `callback` function is an array of objects with these properties:

  + `certUsage`
  + `selector`
  + `match`
  + `data`

  ```
  {
    certUsage: 3,
    selector: 1,
    match: 1,
    data: [ArrayBuffer]
  }
  ```

  ### namespace [resolveTlsa](https://bun.com/reference/node/dns/resolveTlsa)
* function [resolveTxt](https://bun.com/reference/node/dns/resolveTxt)(

  hostname: string,

  callback: (err: null | ErrnoException, addresses: string[][]) => void

  ): void;

  Uses the DNS protocol to resolve text queries (`TXT` records) for the `hostname`. The `records` argument passed to the `callback` function is a two-dimensional array of the text records available for `hostname` (e.g.`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`). Each sub-array contains TXT chunks of one record. Depending on the use case, these could be either joined together or treated separately.

  ### namespace [resolveTxt](https://bun.com/reference/node/dns/resolveTxt)
* ### interface [AnyAaaaRecord](https://bun.com/reference/node/dns/AnyAaaaRecord)

  + [address](https://bun.com/reference/node/dns/AnyAaaaRecord/address): string
  + [ttl](https://bun.com/reference/node/dns/AnyAaaaRecord/ttl): number
  + [type](https://bun.com/reference/node/dns/AnyAaaaRecord/type): 'AAAA'
* ### interface [AnyARecord](https://bun.com/reference/node/dns/AnyARecord)

  + [address](https://bun.com/reference/node/dns/AnyARecord/address): string
  + [ttl](https://bun.com/reference/node/dns/AnyARecord/ttl): number
  + [type](https://bun.com/reference/node/dns/AnyARecord/type): 'A'
* ### interface [AnyCaaRecord](https://bun.com/reference/node/dns/AnyCaaRecord)

  + [contactemail](https://bun.com/reference/node/dns/AnyCaaRecord/contactemail)?: string
  + [contactphone](https://bun.com/reference/node/dns/AnyCaaRecord/contactphone)?: string
  + [critical](https://bun.com/reference/node/dns/AnyCaaRecord/critical): number
  + [iodef](https://bun.com/reference/node/dns/AnyCaaRecord/iodef)?: string
  + [issue](https://bun.com/reference/node/dns/AnyCaaRecord/issue)?: string
  + [issuewild](https://bun.com/reference/node/dns/AnyCaaRecord/issuewild)?: string
  + [type](https://bun.com/reference/node/dns/AnyCaaRecord/type): 'CAA'
* ### interface [AnyCnameRecord](https://bun.com/reference/node/dns/AnyCnameRecord)

  + [type](https://bun.com/reference/node/dns/AnyCnameRecord/type): 'CNAME'
  + [value](https://bun.com/reference/node/dns/AnyCnameRecord/value): string
* ### interface [AnyMxRecord](https://bun.com/reference/node/dns/AnyMxRecord)

  + [exchange](https://bun.com/reference/node/dns/AnyMxRecord/exchange): string
  + [priority](https://bun.com/reference/node/dns/AnyMxRecord/priority): number
  + [type](https://bun.com/reference/node/dns/AnyMxRecord/type): 'MX'
* ### interface [AnyNaptrRecord](https://bun.com/reference/node/dns/AnyNaptrRecord)

  + [flags](https://bun.com/reference/node/dns/AnyNaptrRecord/flags): string
  + [order](https://bun.com/reference/node/dns/AnyNaptrRecord/order): number
  + [preference](https://bun.com/reference/node/dns/AnyNaptrRecord/preference): number
  + [regexp](https://bun.com/reference/node/dns/AnyNaptrRecord/regexp): string
  + [replacement](https://bun.com/reference/node/dns/AnyNaptrRecord/replacement): string
  + [service](https://bun.com/reference/node/dns/AnyNaptrRecord/service): string
  + [type](https://bun.com/reference/node/dns/AnyNaptrRecord/type): 'NAPTR'
* ### interface [AnyNsRecord](https://bun.com/reference/node/dns/AnyNsRecord)

  + [type](https://bun.com/reference/node/dns/AnyNsRecord/type): 'NS'
  + [value](https://bun.com/reference/node/dns/AnyNsRecord/value): string
* ### interface [AnyPtrRecord](https://bun.com/reference/node/dns/AnyPtrRecord)

  + [type](https://bun.com/reference/node/dns/AnyPtrRecord/type): 'PTR'
  + [value](https://bun.com/reference/node/dns/AnyPtrRecord/value): string
* ### interface [AnySoaRecord](https://bun.com/reference/node/dns/AnySoaRecord)

  + [expire](https://bun.com/reference/node/dns/AnySoaRecord/expire): number
  + [hostmaster](https://bun.com/reference/node/dns/AnySoaRecord/hostmaster): string
  + [minttl](https://bun.com/reference/node/dns/AnySoaRecord/minttl): number
  + [nsname](https://bun.com/reference/node/dns/AnySoaRecord/nsname): string
  + [refresh](https://bun.com/reference/node/dns/AnySoaRecord/refresh): number
  + [retry](https://bun.com/reference/node/dns/AnySoaRecord/retry): number
  + [serial](https://bun.com/reference/node/dns/AnySoaRecord/serial): number
  + [type](https://bun.com/reference/node/dns/AnySoaRecord/type): 'SOA'
* ### interface [AnySrvRecord](https://bun.com/reference/node/dns/AnySrvRecord)

  + [name](https://bun.com/reference/node/dns/AnySrvRecord/name): string
  + [port](https://bun.com/reference/node/dns/AnySrvRecord/port): number
  + [priority](https://bun.com/reference/node/dns/AnySrvRecord/priority): number
  + [type](https://bun.com/reference/node/dns/AnySrvRecord/type): 'SRV'
  + [weight](https://bun.com/reference/node/dns/AnySrvRecord/weight): number
* ### interface [AnyTlsaRecord](https://bun.com/reference/node/dns/AnyTlsaRecord)

  + [certUsage](https://bun.com/reference/node/dns/AnyTlsaRecord/certUsage): number
  + [data](https://bun.com/reference/node/dns/AnyTlsaRecord/data): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)
  + [match](https://bun.com/reference/node/dns/AnyTlsaRecord/match): number
  + [selector](https://bun.com/reference/node/dns/AnyTlsaRecord/selector): number
  + [type](https://bun.com/reference/node/dns/AnyTlsaRecord/type): 'TLSA'
* ### interface [AnyTxtRecord](https://bun.com/reference/node/dns/AnyTxtRecord)

  + [entries](https://bun.com/reference/node/dns/AnyTxtRecord/entries): string[]
  + [type](https://bun.com/reference/node/dns/AnyTxtRecord/type): 'TXT'
* ### interface [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)

  + [contactemail](https://bun.com/reference/node/dns/CaaRecord/contactemail)?: string
  + [contactphone](https://bun.com/reference/node/dns/CaaRecord/contactphone)?: string
  + [critical](https://bun.com/reference/node/dns/CaaRecord/critical): number
  + [iodef](https://bun.com/reference/node/dns/CaaRecord/iodef)?: string
  + [issue](https://bun.com/reference/node/dns/CaaRecord/issue)?: string
  + [issuewild](https://bun.com/reference/node/dns/CaaRecord/issuewild)?: string
* ### interface [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)

  + [address](https://bun.com/reference/node/dns/LookupAddress/address): string

    A string representation of an IPv4 or IPv6 address.
  + [family](https://bun.com/reference/node/dns/LookupAddress/family): number

    `4` or `6`, denoting the family of `address`, or `0` if the address is not an IPv4 or IPv6 address. `0` is a likely indicator of a bug in the name resolution service used by the operating system.
* ### interface [LookupAllOptions](https://bun.com/reference/node/dns/LookupAllOptions)

  + [all](https://bun.com/reference/node/dns/LookupAllOptions/all): true

    When `true`, the callback returns all resolved addresses in an array. Otherwise, returns a single address.
  + [family](https://bun.com/reference/node/dns/LookupAllOptions/family)?: number | 'IPv4' | 'IPv6'

    The record family. Must be `4`, `6`, or `0`. For backward compatibility reasons, `'IPv4'` and `'IPv6'` are interpreted as `4` and `6` respectively. The value 0 indicates that either an IPv4 or IPv6 address is returned. If the value `0` is used with `{ all: true } (see below)`, both IPv4 and IPv6 addresses are returned.
  + [hints](https://bun.com/reference/node/dns/LookupAllOptions/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [order](https://bun.com/reference/node/dns/LookupAllOptions/order)?: 'ipv4first' | 'ipv6first' | 'verbatim'

    When `verbatim`, the resolved addresses are return unsorted. When `ipv4first`, the resolved addresses are sorted by placing IPv4 addresses before IPv6 addresses. When `ipv6first`, the resolved addresses are sorted by placing IPv6 addresses before IPv4 addresses. Default value is configurable using setDefaultResultOrder or [`--dns-result-order`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--dns-result-orderorder).
* ### interface [LookupOneOptions](https://bun.com/reference/node/dns/LookupOneOptions)

  + [all](https://bun.com/reference/node/dns/LookupOneOptions/all)?: false

    When `true`, the callback returns all resolved addresses in an array. Otherwise, returns a single address.
  + [family](https://bun.com/reference/node/dns/LookupOneOptions/family)?: number | 'IPv4' | 'IPv6'

    The record family. Must be `4`, `6`, or `0`. For backward compatibility reasons, `'IPv4'` and `'IPv6'` are interpreted as `4` and `6` respectively. The value 0 indicates that either an IPv4 or IPv6 address is returned. If the value `0` is used with `{ all: true } (see below)`, both IPv4 and IPv6 addresses are returned.
  + [hints](https://bun.com/reference/node/dns/LookupOneOptions/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [order](https://bun.com/reference/node/dns/LookupOneOptions/order)?: 'ipv4first' | 'ipv6first' | 'verbatim'

    When `verbatim`, the resolved addresses are return unsorted. When `ipv4first`, the resolved addresses are sorted by placing IPv4 addresses before IPv6 addresses. When `ipv6first`, the resolved addresses are sorted by placing IPv6 addresses before IPv4 addresses. Default value is configurable using setDefaultResultOrder or [`--dns-result-order`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--dns-result-orderorder).
* ### interface [LookupOptions](https://bun.com/reference/node/dns/LookupOptions)

  + [all](https://bun.com/reference/node/dns/LookupOptions/all)?: boolean

    When `true`, the callback returns all resolved addresses in an array. Otherwise, returns a single address.
  + [family](https://bun.com/reference/node/dns/LookupOptions/family)?: number | 'IPv4' | 'IPv6'

    The record family. Must be `4`, `6`, or `0`. For backward compatibility reasons, `'IPv4'` and `'IPv6'` are interpreted as `4` and `6` respectively. The value 0 indicates that either an IPv4 or IPv6 address is returned. If the value `0` is used with `{ all: true } (see below)`, both IPv4 and IPv6 addresses are returned.
  + [hints](https://bun.com/reference/node/dns/LookupOptions/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [order](https://bun.com/reference/node/dns/LookupOptions/order)?: 'ipv4first' | 'ipv6first' | 'verbatim'

    When `verbatim`, the resolved addresses are return unsorted. When `ipv4first`, the resolved addresses are sorted by placing IPv4 addresses before IPv6 addresses. When `ipv6first`, the resolved addresses are sorted by placing IPv6 addresses before IPv4 addresses. Default value is configurable using setDefaultResultOrder or [`--dns-result-order`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--dns-result-orderorder).
* ### interface [MxRecord](https://bun.com/reference/node/dns/MxRecord)

  + [exchange](https://bun.com/reference/node/dns/MxRecord/exchange): string
  + [priority](https://bun.com/reference/node/dns/MxRecord/priority): number
* ### interface [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)

  + [flags](https://bun.com/reference/node/dns/NaptrRecord/flags): string
  + [order](https://bun.com/reference/node/dns/NaptrRecord/order): number
  + [preference](https://bun.com/reference/node/dns/NaptrRecord/preference): number
  + [regexp](https://bun.com/reference/node/dns/NaptrRecord/regexp): string
  + [replacement](https://bun.com/reference/node/dns/NaptrRecord/replacement): string
  + [service](https://bun.com/reference/node/dns/NaptrRecord/service): string
* ### interface [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)

  + [address](https://bun.com/reference/node/dns/RecordWithTtl/address): string
  + [ttl](https://bun.com/reference/node/dns/RecordWithTtl/ttl): number
* ### interface [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions)

  + [ttl](https://bun.com/reference/node/dns/ResolveOptions/ttl): boolean
* ### interface [ResolverOptions](https://bun.com/reference/node/dns/ResolverOptions)

  + [maxTimeout](https://bun.com/reference/node/dns/ResolverOptions/maxTimeout)?: number

    The max retry timeout, in milliseconds.
  + [timeout](https://bun.com/reference/node/dns/ResolverOptions/timeout)?: number

    Query timeout in milliseconds, or `-1` to use the default timeout.
  + [tries](https://bun.com/reference/node/dns/ResolverOptions/tries)?: number

    The number of tries the resolver will try contacting each name server before giving up.
* ### interface [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions)

  + [ttl](https://bun.com/reference/node/dns/ResolveWithTtlOptions/ttl): true
* ### interface [SoaRecord](https://bun.com/reference/node/dns/SoaRecord)

  + [expire](https://bun.com/reference/node/dns/SoaRecord/expire): number
  + [hostmaster](https://bun.com/reference/node/dns/SoaRecord/hostmaster): string
  + [minttl](https://bun.com/reference/node/dns/SoaRecord/minttl): number
  + [nsname](https://bun.com/reference/node/dns/SoaRecord/nsname): string
  + [refresh](https://bun.com/reference/node/dns/SoaRecord/refresh): number
  + [retry](https://bun.com/reference/node/dns/SoaRecord/retry): number
  + [serial](https://bun.com/reference/node/dns/SoaRecord/serial): number
* ### interface [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)

  + [name](https://bun.com/reference/node/dns/SrvRecord/name): string
  + [port](https://bun.com/reference/node/dns/SrvRecord/port): number
  + [priority](https://bun.com/reference/node/dns/SrvRecord/priority): number
  + [weight](https://bun.com/reference/node/dns/SrvRecord/weight): number
* ### interface [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)

  + [certUsage](https://bun.com/reference/node/dns/TlsaRecord/certUsage): number
  + [data](https://bun.com/reference/node/dns/TlsaRecord/data): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)
  + [match](https://bun.com/reference/node/dns/TlsaRecord/match): number
  + [selector](https://bun.com/reference/node/dns/TlsaRecord/selector): number
* type [AnyRecord](https://bun.com/reference/node/dns/AnyRecord) = [AnyARecord](https://bun.com/reference/node/dns/AnyARecord) | [AnyAaaaRecord](https://bun.com/reference/node/dns/AnyAaaaRecord) | [AnyCaaRecord](https://bun.com/reference/node/dns/AnyCaaRecord) | [AnyCnameRecord](https://bun.com/reference/node/dns/AnyCnameRecord) | [AnyMxRecord](https://bun.com/reference/node/dns/AnyMxRecord) | [AnyNaptrRecord](https://bun.com/reference/node/dns/AnyNaptrRecord) | [AnyNsRecord](https://bun.com/reference/node/dns/AnyNsRecord) | [AnyPtrRecord](https://bun.com/reference/node/dns/AnyPtrRecord) | [AnySoaRecord](https://bun.com/reference/node/dns/AnySoaRecord) | [AnySrvRecord](https://bun.com/reference/node/dns/AnySrvRecord) | [AnyTlsaRecord](https://bun.com/reference/node/dns/AnyTlsaRecord) | [AnyTxtRecord](https://bun.com/reference/node/dns/AnyTxtRecord)