---
url: https://bun.com/reference/node/dns/promises
title: Node.js dns/promises module | API Reference | Bun
source_domain: bun.com
---

# Node.js dns/promises module | API Reference | Bun

Node.js module

# [dns/promises](https://bun.com/reference/node/dns/promises)

The `'node:dns/promises'` module offers the same DNS resolution API as `node:dns` but returns `Promise`-based methods for cleaner async/await usage.

All lookup and resolve functions are available as promise-returning calls, eliminating the need for callback-based code.

* ### class [Resolver](https://bun.com/reference/node/dns/promises/Resolver)

  An independent resolver for DNS requests.

  Creating a new resolver uses the default server settings. Setting the servers used for a resolver using [`resolver.setServers()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromisessetserversservers) does not affect other resolvers:

  ```
  import { promises } from 'node:dns';
  const resolver = new promises.Resolver();
  resolver.setServers(['4.4.4.4']);

  // This request will use the server at 4.4.4.4, independent of global settings.
  resolver.resolve4('example.org').then((addresses) => {
    // ...
  });

  // Alternatively, the same code can be written using async-await style.
  (async function() {
    const addresses = await resolver.resolve4('example.org');
  })();
  ```

  The following methods from the `dnsPromises` API are available:

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

  + [getServers](https://bun.com/reference/node/dns/promises/Resolver/getServers): () => string[]
  + [resolve](https://bun.com/reference/node/dns/promises/Resolver/resolve): {(hostname: string) => Promise<string[]>; (hostname: string, rrtype: 'A' | 'AAAA' | 'CNAME' | 'NS' | 'PTR') => Promise<string[]>; (hostname: string, rrtype: 'ANY') => Promise<[AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]>; (hostname: string, rrtype: 'CAA') => Promise<[CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]>; (hostname: string, rrtype: 'MX') => Promise<[MxRecord](https://bun.com/reference/node/dns/MxRecord)[]>; (hostname: string, rrtype: 'NAPTR') => Promise<[NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]>; (hostname: string, rrtype: 'SOA') => Promise<[SoaRecord](https://bun.com/reference/node/dns/SoaRecord)>; (hostname: string, rrtype: 'SRV') => Promise<[SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]>; (hostname: string, rrtype: 'TLSA') => Promise<[TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]>; (hostname: string, rrtype: 'TXT') => Promise<string[][]>; (hostname: string, rrtype: string) => Promise<string[] | [SoaRecord](https://bun.com/reference/node/dns/SoaRecord) | [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[] | [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[] | [MxRecord](https://bun.com/reference/node/dns/MxRecord)[] | [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[] | [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[] | [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[] | string[][]>}
  + [resolve4](https://bun.com/reference/node/dns/promises/Resolver/resolve4): {(hostname: string) => Promise<string[]>; (hostname: string, options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions)) => Promise<[RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>; (hostname: string, options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions)) => Promise<string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>}
  + [resolve6](https://bun.com/reference/node/dns/promises/Resolver/resolve6): {(hostname: string) => Promise<string[]>; (hostname: string, options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions)) => Promise<[RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>; (hostname: string, options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions)) => Promise<string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>}
  + [resolveAny](https://bun.com/reference/node/dns/promises/Resolver/resolveAny): (hostname: string) => Promise<[AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]>
  + [resolveCaa](https://bun.com/reference/node/dns/promises/Resolver/resolveCaa): (hostname: string) => Promise<[CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]>
  + [resolveCname](https://bun.com/reference/node/dns/promises/Resolver/resolveCname): (hostname: string) => Promise<string[]>
  + [resolveMx](https://bun.com/reference/node/dns/promises/Resolver/resolveMx): (hostname: string) => Promise<[MxRecord](https://bun.com/reference/node/dns/MxRecord)[]>
  + [resolveNaptr](https://bun.com/reference/node/dns/promises/Resolver/resolveNaptr): (hostname: string) => Promise<[NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]>
  + [resolveNs](https://bun.com/reference/node/dns/promises/Resolver/resolveNs): (hostname: string) => Promise<string[]>
  + [resolvePtr](https://bun.com/reference/node/dns/promises/Resolver/resolvePtr): (hostname: string) => Promise<string[]>
  + [resolveSoa](https://bun.com/reference/node/dns/promises/Resolver/resolveSoa): (hostname: string) => Promise<[SoaRecord](https://bun.com/reference/node/dns/SoaRecord)>
  + [resolveSrv](https://bun.com/reference/node/dns/promises/Resolver/resolveSrv): (hostname: string) => Promise<[SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]>
  + [resolveTlsa](https://bun.com/reference/node/dns/promises/Resolver/resolveTlsa): (hostname: string) => Promise<[TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]>
  + [resolveTxt](https://bun.com/reference/node/dns/promises/Resolver/resolveTxt): (hostname: string) => Promise<string[][]>
  + [reverse](https://bun.com/reference/node/dns/promises/Resolver/reverse): (ip: string) => Promise<string[]>
  + [setServers](https://bun.com/reference/node/dns/promises/Resolver/setServers): (servers: readonly string[]) => void
  + [cancel](https://bun.com/reference/node/dns/promises/Resolver/cancel)(): void;

    Cancel all outstanding DNS queries made by this resolver. The corresponding callbacks will be called with an error with code `ECANCELLED`.
  + [setLocalAddress](https://bun.com/reference/node/dns/promises/Resolver/setLocalAddress)(

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
* const [ADDRGETNETWORKPARAMS](https://bun.com/reference/node/dns/promises/ADDRGETNETWORKPARAMS): 'EADDRGETNETWORKPARAMS'
* const [BADFAMILY](https://bun.com/reference/node/dns/promises/BADFAMILY): 'EBADFAMILY'
* const [BADFLAGS](https://bun.com/reference/node/dns/promises/BADFLAGS): 'EBADFLAGS'
* const [BADHINTS](https://bun.com/reference/node/dns/promises/BADHINTS): 'EBADHINTS'
* const [BADNAME](https://bun.com/reference/node/dns/promises/BADNAME): 'EBADNAME'
* const [BADQUERY](https://bun.com/reference/node/dns/promises/BADQUERY): 'EBADQUERY'
* const [BADRESP](https://bun.com/reference/node/dns/promises/BADRESP): 'EBADRESP'
* const [BADSTR](https://bun.com/reference/node/dns/promises/BADSTR): 'EBADSTR'
* const [CANCELLED](https://bun.com/reference/node/dns/promises/CANCELLED): 'ECANCELLED'
* const [CONNREFUSED](https://bun.com/reference/node/dns/promises/CONNREFUSED): 'ECONNREFUSED'
* const [DESTRUCTION](https://bun.com/reference/node/dns/promises/DESTRUCTION): 'EDESTRUCTION'
* const [EOF](https://bun.com/reference/node/dns/promises/EOF): 'EOF'
* const [FILE](https://bun.com/reference/node/dns/promises/FILE): 'EFILE'
* const [FORMERR](https://bun.com/reference/node/dns/promises/FORMERR): 'EFORMERR'
* const [LOADIPHLPAPI](https://bun.com/reference/node/dns/promises/LOADIPHLPAPI): 'ELOADIPHLPAPI'
* const [NODATA](https://bun.com/reference/node/dns/promises/NODATA): 'ENODATA'
* const [NOMEM](https://bun.com/reference/node/dns/promises/NOMEM): 'ENOMEM'
* const [NONAME](https://bun.com/reference/node/dns/promises/NONAME): 'ENONAME'
* const [NOTFOUND](https://bun.com/reference/node/dns/promises/NOTFOUND): 'ENOTFOUND'
* const [NOTIMP](https://bun.com/reference/node/dns/promises/NOTIMP): 'ENOTIMP'
* const [NOTINITIALIZED](https://bun.com/reference/node/dns/promises/NOTINITIALIZED): 'ENOTINITIALIZED'
* const [REFUSED](https://bun.com/reference/node/dns/promises/REFUSED): 'EREFUSED'
* const [SERVFAIL](https://bun.com/reference/node/dns/promises/SERVFAIL): 'ESERVFAIL'
* const [TIMEOUT](https://bun.com/reference/node/dns/promises/TIMEOUT): 'ETIMEOUT'
* function [getDefaultResultOrder](https://bun.com/reference/node/dns/promises/getDefaultResultOrder)(): 'ipv4first' | 'verbatim';

  Get the default value for `verbatim` in lookup and [dnsPromises.lookup()](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options). The value could be:

  + `ipv4first`: for `verbatim` defaulting to `false`.
  + `verbatim`: for `verbatim` defaulting to `true`.
* function [getServers](https://bun.com/reference/node/dns/promises/getServers)(): string[];

  Returns an array of IP address strings, formatted according to [RFC 5952](https://tools.ietf.org/html/rfc5952#section-6), that are currently configured for DNS resolution. A string will include a port section if a custom port is used.

  ```
  [
    '4.4.4.4',
    '2001:4860:4860::8888',
    '4.4.4.4:1053',
    '[2001:4860:4860::8888]:1053',
  ]
  ```
* function [lookup](https://bun.com/reference/node/dns/promises/lookup)(

  hostname: string,

  family: number

  ): Promise<[LookupAddress](https://bun.com/reference/node/dns/LookupAddress)>;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the `Promise` is resolved with `addresses` being an array of objects with the properties `address` and `family`.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options) does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v20.x/api/dns.html#implementation-considerations) before using `dnsPromises.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const dnsPromises = dns.promises;
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };

  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('address: %j family: IPv%s', result.address, result.family);
    // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
  });

  // When options.all is true, the result will be an Array.
  options.all = true;
  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('addresses: %j', result);
    // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  });
  ```

  function [lookup](https://bun.com/reference/node/dns/promises/lookup)(

  hostname: string,

  options: [LookupOneOptions](https://bun.com/reference/node/dns/LookupOneOptions)

  ): Promise<[LookupAddress](https://bun.com/reference/node/dns/LookupAddress)>;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the `Promise` is resolved with `addresses` being an array of objects with the properties `address` and `family`.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options) does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v20.x/api/dns.html#implementation-considerations) before using `dnsPromises.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const dnsPromises = dns.promises;
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };

  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('address: %j family: IPv%s', result.address, result.family);
    // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
  });

  // When options.all is true, the result will be an Array.
  options.all = true;
  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('addresses: %j', result);
    // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  });
  ```

  function [lookup](https://bun.com/reference/node/dns/promises/lookup)(

  hostname: string,

  options: [LookupAllOptions](https://bun.com/reference/node/dns/LookupAllOptions)

  ): Promise<[LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[]>;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the `Promise` is resolved with `addresses` being an array of objects with the properties `address` and `family`.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options) does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v20.x/api/dns.html#implementation-considerations) before using `dnsPromises.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const dnsPromises = dns.promises;
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };

  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('address: %j family: IPv%s', result.address, result.family);
    // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
  });

  // When options.all is true, the result will be an Array.
  options.all = true;
  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('addresses: %j', result);
    // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  });
  ```

  function [lookup](https://bun.com/reference/node/dns/promises/lookup)(

  hostname: string,

  options: [LookupOptions](https://bun.com/reference/node/dns/LookupOptions)

  ): Promise<[LookupAddress](https://bun.com/reference/node/dns/LookupAddress) | [LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[]>;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the `Promise` is resolved with `addresses` being an array of objects with the properties `address` and `family`.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options) does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v20.x/api/dns.html#implementation-considerations) before using `dnsPromises.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const dnsPromises = dns.promises;
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };

  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('address: %j family: IPv%s', result.address, result.family);
    // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
  });

  // When options.all is true, the result will be an Array.
  options.all = true;
  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('addresses: %j', result);
    // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  });
  ```

  function [lookup](https://bun.com/reference/node/dns/promises/lookup)(

  hostname: string

  ): Promise<[LookupAddress](https://bun.com/reference/node/dns/LookupAddress)>;

  Resolves a host name (e.g. `'nodejs.org'`) into the first found A (IPv4) or AAAA (IPv6) record. All `option` properties are optional. If `options` is an integer, then it must be `4` or `6` – if `options` is not provided, then IPv4 and IPv6 addresses are both returned if found.

  With the `all` option set to `true`, the `Promise` is resolved with `addresses` being an array of objects with the properties `address` and `family`.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code. Keep in mind that `err.code` will be set to `'ENOTFOUND'` not only when the host name does not exist but also when the lookup fails in other ways such as no available file descriptors.

  [`dnsPromises.lookup()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromiseslookuphostname-options) does not necessarily have anything to do with the DNS protocol. The implementation uses an operating system facility that can associate names with addresses and vice versa. This implementation can have subtle but important consequences on the behavior of any Node.js program. Please take some time to consult the [Implementation considerations section](https://nodejs.org/docs/latest-v20.x/api/dns.html#implementation-considerations) before using `dnsPromises.lookup()`.

  Example usage:

  ```
  import dns from 'node:dns';
  const dnsPromises = dns.promises;
  const options = {
    family: 6,
    hints: dns.ADDRCONFIG | dns.V4MAPPED,
  };

  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('address: %j family: IPv%s', result.address, result.family);
    // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
  });

  // When options.all is true, the result will be an Array.
  options.all = true;
  dnsPromises.lookup('example.com', options).then((result) => {
    console.log('addresses: %j', result);
    // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
  });
  ```
* function [lookupService](https://bun.com/reference/node/dns/promises/lookupService)(

  address: string,

  port: number

  ): Promise<{ hostname: string; service: string }>;

  Resolves the given `address` and `port` into a host name and service using the operating system's underlying `getnameinfo` implementation.

  If `address` is not a valid IP address, a `TypeError` will be thrown. The `port` will be coerced to a number. If it is not a legal port, a `TypeError` will be thrown.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is the error code.

  ```
  import dnsPromises from 'node:dns';
  dnsPromises.lookupService('127.0.0.1', 22).then((result) => {
    console.log(result.hostname, result.service);
    // Prints: localhost ssh
  });
  ```
* function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'A' | 'AAAA' | 'CNAME' | 'NS' | 'PTR'

  ): Promise<string[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'ANY'

  ): Promise<[AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'CAA'

  ): Promise<[CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'MX'

  ): Promise<[MxRecord](https://bun.com/reference/node/dns/MxRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'NAPTR'

  ): Promise<[NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'SOA'

  ): Promise<[SoaRecord](https://bun.com/reference/node/dns/SoaRecord)>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'SRV'

  ): Promise<[SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'TLSA'

  ): Promise<[TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: 'TXT'

  ): Promise<string[][]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.

  function [resolve](https://bun.com/reference/node/dns/promises/resolve)(

  hostname: string,

  rrtype: string

  ): Promise<string[] | [SoaRecord](https://bun.com/reference/node/dns/SoaRecord) | [AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[] | [CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[] | [MxRecord](https://bun.com/reference/node/dns/MxRecord)[] | [NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[] | [SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[] | [TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[] | string[][]>;

  Uses the DNS protocol to resolve a host name (e.g. `'nodejs.org'`) into an array of the resource records. When successful, the `Promise` is resolved with an array of resource records. The type and structure of individual results vary based on `rrtype`:

  <omitted>

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).

  @param hostname

  Host name to resolve.

  @param rrtype

  Resource record type.
* function [resolve4](https://bun.com/reference/node/dns/promises/resolve4)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve IPv4 addresses (`A` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv4 addresses (e.g. `['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/promises/resolve4)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions)

  ): Promise<[RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>;

  Uses the DNS protocol to resolve IPv4 addresses (`A` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv4 addresses (e.g. `['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.

  function [resolve4](https://bun.com/reference/node/dns/promises/resolve4)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions)

  ): Promise<string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>;

  Uses the DNS protocol to resolve IPv4 addresses (`A` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv4 addresses (e.g. `['74.125.79.104', '74.125.79.105', '74.125.79.106']`).

  @param hostname

  Host name to resolve.
* function [resolve6](https://bun.com/reference/node/dns/promises/resolve6)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/promises/resolve6)(

  hostname: string,

  options: [ResolveWithTtlOptions](https://bun.com/reference/node/dns/ResolveWithTtlOptions)

  ): Promise<[RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv6 addresses.

  @param hostname

  Host name to resolve.

  function [resolve6](https://bun.com/reference/node/dns/promises/resolve6)(

  hostname: string,

  options: [ResolveOptions](https://bun.com/reference/node/dns/ResolveOptions)

  ): Promise<string[] | [RecordWithTtl](https://bun.com/reference/node/dns/RecordWithTtl)[]>;

  Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the `hostname`. On success, the `Promise` is resolved with an array of IPv6 addresses.

  @param hostname

  Host name to resolve.
* function [resolveAny](https://bun.com/reference/node/dns/promises/resolveAny)(

  hostname: string

  ): Promise<[AnyRecord](https://bun.com/reference/node/dns/AnyRecord)[]>;

  Uses the DNS protocol to resolve all records (also known as `ANY` or `*` query). On success, the `Promise` is resolved with an array containing various types of records. Each object has a property `type` that indicates the type of the current record. And depending on the `type`, additional properties will be present on the object:

  <omitted>

  Here is an example of the result object:

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
* function [resolveCaa](https://bun.com/reference/node/dns/promises/resolveCaa)(

  hostname: string

  ): Promise<[CaaRecord](https://bun.com/reference/node/dns/CaaRecord)[]>;

  Uses the DNS protocol to resolve `CAA` records for the `hostname`. On success, the `Promise` is resolved with an array of objects containing available certification authority authorization records available for the `hostname` (e.g. `[{critical: 0, iodef: 'mailto:pki@example.com'},{critical: 128, issue: 'pki.example.com'}]`).
* function [resolveCname](https://bun.com/reference/node/dns/promises/resolveCname)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve `CNAME` records for the `hostname`. On success, the `Promise` is resolved with an array of canonical name records available for the `hostname` (e.g. `['bar.example.com']`).
* function [resolveMx](https://bun.com/reference/node/dns/promises/resolveMx)(

  hostname: string

  ): Promise<[MxRecord](https://bun.com/reference/node/dns/MxRecord)[]>;

  Uses the DNS protocol to resolve mail exchange records (`MX` records) for the `hostname`. On success, the `Promise` is resolved with an array of objects containing both a `priority` and `exchange` property (e.g.`[{priority: 10, exchange: 'mx.example.com'}, ...]`).
* function [resolveNaptr](https://bun.com/reference/node/dns/promises/resolveNaptr)(

  hostname: string

  ): Promise<[NaptrRecord](https://bun.com/reference/node/dns/NaptrRecord)[]>;

  Uses the DNS protocol to resolve regular expression-based records (`NAPTR` records) for the `hostname`. On success, the `Promise` is resolved with an array of objects with the following properties:

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
* function [resolveNs](https://bun.com/reference/node/dns/promises/resolveNs)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve name server records (`NS` records) for the `hostname`. On success, the `Promise` is resolved with an array of name server records available for `hostname` (e.g.`['ns1.example.com', 'ns2.example.com']`).
* function [resolvePtr](https://bun.com/reference/node/dns/promises/resolvePtr)(

  hostname: string

  ): Promise<string[]>;

  Uses the DNS protocol to resolve pointer records (`PTR` records) for the `hostname`. On success, the `Promise` is resolved with an array of strings containing the reply records.
* function [resolveSoa](https://bun.com/reference/node/dns/promises/resolveSoa)(

  hostname: string

  ): Promise<[SoaRecord](https://bun.com/reference/node/dns/SoaRecord)>;

  Uses the DNS protocol to resolve a start of authority record (`SOA` record) for the `hostname`. On success, the `Promise` is resolved with an object with the following properties:

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
* function [resolveSrv](https://bun.com/reference/node/dns/promises/resolveSrv)(

  hostname: string

  ): Promise<[SrvRecord](https://bun.com/reference/node/dns/SrvRecord)[]>;

  Uses the DNS protocol to resolve service records (`SRV` records) for the `hostname`. On success, the `Promise` is resolved with an array of objects with the following properties:

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
* function [resolveTlsa](https://bun.com/reference/node/dns/promises/resolveTlsa)(

  hostname: string

  ): Promise<[TlsaRecord](https://bun.com/reference/node/dns/TlsaRecord)[]>;

  Uses the DNS protocol to resolve certificate associations (`TLSA` records) for the `hostname`. On success, the `Promise` is resolved with an array of objectsAdd commentMore actions with these properties:

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
* function [resolveTxt](https://bun.com/reference/node/dns/promises/resolveTxt)(

  hostname: string

  ): Promise<string[][]>;

  Uses the DNS protocol to resolve text queries (`TXT` records) for the `hostname`. On success, the `Promise` is resolved with a two-dimensional array of the text records available for `hostname` (e.g.`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`). Each sub-array contains TXT chunks of one record. Depending on the use case, these could be either joined together or treated separately.
* function [reverse](https://bun.com/reference/node/dns/promises/reverse)(

  ip: string

  ): Promise<string[]>;

  Performs a reverse DNS query that resolves an IPv4 or IPv6 address to an array of host names.

  On error, the `Promise` is rejected with an [`Error`](https://nodejs.org/docs/latest-v20.x/api/errors.html#class-error) object, where `err.code` is one of the [DNS error codes](https://nodejs.org/docs/latest-v20.x/api/dns.html#error-codes).
* function [setDefaultResultOrder](https://bun.com/reference/node/dns/promises/setDefaultResultOrder)(

  order: 'ipv4first' | 'ipv6first' | 'verbatim'

  ): void;

  Set the default value of `order` in `dns.lookup()` and `{@link lookup}`. The value could be:

  + `ipv4first`: sets default `order` to `ipv4first`.
  + `ipv6first`: sets default `order` to `ipv6first`.
  + `verbatim`: sets default `order` to `verbatim`.

  The default is `verbatim` and [dnsPromises.setDefaultResultOrder()](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromisessetdefaultresultorderorder) have higher priority than [`--dns-result-order`](https://nodejs.org/docs/latest-v20.x/api/cli.html#--dns-result-orderorder). When using [worker threads](https://nodejs.org/docs/latest-v20.x/api/worker_threads.html), [`dnsPromises.setDefaultResultOrder()`](https://nodejs.org/docs/latest-v20.x/api/dns.html#dnspromisessetdefaultresultorderorder) from the main thread won't affect the default dns orders in workers.

  @param order

  must be `'ipv4first'`, `'ipv6first'` or `'verbatim'`.
* function [setServers](https://bun.com/reference/node/dns/promises/setServers)(

  servers: readonly string[]

  ): void;

  Sets the IP address and port of servers to be used when performing DNS resolution. The `servers` argument is an array of [RFC 5952](https://tools.ietf.org/html/rfc5952#section-6) formatted addresses. If the port is the IANA default DNS port (53) it can be omitted.

  ```
  dnsPromises.setServers([
    '4.4.4.4',
    '[2001:4860:4860::8888]',
    '4.4.4.4:1053',
    '[2001:4860:4860::8888]:1053',
  ]);
  ```

  An error will be thrown if an invalid address is provided.

  The `dnsPromises.setServers()` method must not be called while a DNS query is in progress.

  This method works much like [resolve.conf](https://man7.org/linux/man-pages/man5/resolv.conf.5.html). That is, if attempting to resolve with the first server provided results in a `NOTFOUND` error, the `resolve()` method will *not* attempt to resolve with subsequent servers provided. Fallback DNS servers will only be used if the earlier ones time out or result in some other error.

  @param servers

  array of `RFC 5952` formatted addresses