---
url: https://bun.com/reference/node/os
title: Node.js os module | API Reference | Bun
source_domain: bun.com
---

# Node.js os module | API Reference | Bun

Node.js module

# [os](https://bun.com/reference/node/os)

The `'node:os'` module provides operating system-related utility methods and properties, such as CPU architecture, memory usage, uptime, user information, network interfaces, and platform details.

It is useful for gathering runtime environment data and making OS-specific decisions.

Works in Bun

Fully implemented. 100% of Node.js's test suite passes.

* ### namespace [constants](https://bun.com/reference/node/os/constants)

  + ### namespace [dlopen](https://bun.com/reference/node/os/constants/dlopen)

    - const [RTLD\_DEEPBIND](https://bun.com/reference/node/os/constants/dlopen/RTLD_DEEPBIND): number
    - const [RTLD\_GLOBAL](https://bun.com/reference/node/os/constants/dlopen/RTLD_GLOBAL): number
    - const [RTLD\_LAZY](https://bun.com/reference/node/os/constants/dlopen/RTLD_LAZY): number
    - const [RTLD\_LOCAL](https://bun.com/reference/node/os/constants/dlopen/RTLD_LOCAL): number
    - const [RTLD\_NOW](https://bun.com/reference/node/os/constants/dlopen/RTLD_NOW): number
  + ### namespace [errno](https://bun.com/reference/node/os/constants/errno)

    - const [E2BIG](https://bun.com/reference/node/os/constants/errno/E2BIG): number
    - const [EACCES](https://bun.com/reference/node/os/constants/errno/EACCES): number
    - const [EADDRINUSE](https://bun.com/reference/node/os/constants/errno/EADDRINUSE): number
    - const [EADDRNOTAVAIL](https://bun.com/reference/node/os/constants/errno/EADDRNOTAVAIL): number
    - const [EAFNOSUPPORT](https://bun.com/reference/node/os/constants/errno/EAFNOSUPPORT): number
    - const [EAGAIN](https://bun.com/reference/node/os/constants/errno/EAGAIN): number
    - const [EALREADY](https://bun.com/reference/node/os/constants/errno/EALREADY): number
    - const [EBADF](https://bun.com/reference/node/os/constants/errno/EBADF): number
    - const [EBADMSG](https://bun.com/reference/node/os/constants/errno/EBADMSG): number
    - const [EBUSY](https://bun.com/reference/node/os/constants/errno/EBUSY): number
    - const [ECANCELED](https://bun.com/reference/node/os/constants/errno/ECANCELED): number
    - const [ECHILD](https://bun.com/reference/node/os/constants/errno/ECHILD): number
    - const [ECONNABORTED](https://bun.com/reference/node/os/constants/errno/ECONNABORTED): number
    - const [ECONNREFUSED](https://bun.com/reference/node/os/constants/errno/ECONNREFUSED): number
    - const [ECONNRESET](https://bun.com/reference/node/os/constants/errno/ECONNRESET): number
    - const [EDEADLK](https://bun.com/reference/node/os/constants/errno/EDEADLK): number
    - const [EDESTADDRREQ](https://bun.com/reference/node/os/constants/errno/EDESTADDRREQ): number
    - const [EDOM](https://bun.com/reference/node/os/constants/errno/EDOM): number
    - const [EDQUOT](https://bun.com/reference/node/os/constants/errno/EDQUOT): number
    - const [EEXIST](https://bun.com/reference/node/os/constants/errno/EEXIST): number
    - const [EFAULT](https://bun.com/reference/node/os/constants/errno/EFAULT): number
    - const [EFBIG](https://bun.com/reference/node/os/constants/errno/EFBIG): number
    - const [EHOSTUNREACH](https://bun.com/reference/node/os/constants/errno/EHOSTUNREACH): number
    - const [EIDRM](https://bun.com/reference/node/os/constants/errno/EIDRM): number
    - const [EILSEQ](https://bun.com/reference/node/os/constants/errno/EILSEQ): number
    - const [EINPROGRESS](https://bun.com/reference/node/os/constants/errno/EINPROGRESS): number
    - const [EINTR](https://bun.com/reference/node/os/constants/errno/EINTR): number
    - const [EINVAL](https://bun.com/reference/node/os/constants/errno/EINVAL): number
    - const [EIO](https://bun.com/reference/node/os/constants/errno/EIO): number
    - const [EISCONN](https://bun.com/reference/node/os/constants/errno/EISCONN): number
    - const [EISDIR](https://bun.com/reference/node/os/constants/errno/EISDIR): number
    - const [ELOOP](https://bun.com/reference/node/os/constants/errno/ELOOP): number
    - const [EMFILE](https://bun.com/reference/node/os/constants/errno/EMFILE): number
    - const [EMLINK](https://bun.com/reference/node/os/constants/errno/EMLINK): number
    - const [EMSGSIZE](https://bun.com/reference/node/os/constants/errno/EMSGSIZE): number
    - const [EMULTIHOP](https://bun.com/reference/node/os/constants/errno/EMULTIHOP): number
    - const [ENAMETOOLONG](https://bun.com/reference/node/os/constants/errno/ENAMETOOLONG): number
    - const [ENETDOWN](https://bun.com/reference/node/os/constants/errno/ENETDOWN): number
    - const [ENETRESET](https://bun.com/reference/node/os/constants/errno/ENETRESET): number
    - const [ENETUNREACH](https://bun.com/reference/node/os/constants/errno/ENETUNREACH): number
    - const [ENFILE](https://bun.com/reference/node/os/constants/errno/ENFILE): number
    - const [ENOBUFS](https://bun.com/reference/node/os/constants/errno/ENOBUFS): number
    - const [ENODATA](https://bun.com/reference/node/os/constants/errno/ENODATA): number
    - const [ENODEV](https://bun.com/reference/node/os/constants/errno/ENODEV): number
    - const [ENOENT](https://bun.com/reference/node/os/constants/errno/ENOENT): number
    - const [ENOEXEC](https://bun.com/reference/node/os/constants/errno/ENOEXEC): number
    - const [ENOLCK](https://bun.com/reference/node/os/constants/errno/ENOLCK): number
    - const [ENOLINK](https://bun.com/reference/node/os/constants/errno/ENOLINK): number
    - const [ENOMEM](https://bun.com/reference/node/os/constants/errno/ENOMEM): number
    - const [ENOMSG](https://bun.com/reference/node/os/constants/errno/ENOMSG): number
    - const [ENOPROTOOPT](https://bun.com/reference/node/os/constants/errno/ENOPROTOOPT): number
    - const [ENOSPC](https://bun.com/reference/node/os/constants/errno/ENOSPC): number
    - const [ENOSR](https://bun.com/reference/node/os/constants/errno/ENOSR): number
    - const [ENOSTR](https://bun.com/reference/node/os/constants/errno/ENOSTR): number
    - const [ENOSYS](https://bun.com/reference/node/os/constants/errno/ENOSYS): number
    - const [ENOTCONN](https://bun.com/reference/node/os/constants/errno/ENOTCONN): number
    - const [ENOTDIR](https://bun.com/reference/node/os/constants/errno/ENOTDIR): number
    - const [ENOTEMPTY](https://bun.com/reference/node/os/constants/errno/ENOTEMPTY): number
    - const [ENOTSOCK](https://bun.com/reference/node/os/constants/errno/ENOTSOCK): number
    - const [ENOTSUP](https://bun.com/reference/node/os/constants/errno/ENOTSUP): number
    - const [ENOTTY](https://bun.com/reference/node/os/constants/errno/ENOTTY): number
    - const [ENXIO](https://bun.com/reference/node/os/constants/errno/ENXIO): number
    - const [EOPNOTSUPP](https://bun.com/reference/node/os/constants/errno/EOPNOTSUPP): number
    - const [EOVERFLOW](https://bun.com/reference/node/os/constants/errno/EOVERFLOW): number
    - const [EPERM](https://bun.com/reference/node/os/constants/errno/EPERM): number
    - const [EPIPE](https://bun.com/reference/node/os/constants/errno/EPIPE): number
    - const [EPROTO](https://bun.com/reference/node/os/constants/errno/EPROTO): number
    - const [EPROTONOSUPPORT](https://bun.com/reference/node/os/constants/errno/EPROTONOSUPPORT): number
    - const [EPROTOTYPE](https://bun.com/reference/node/os/constants/errno/EPROTOTYPE): number
    - const [ERANGE](https://bun.com/reference/node/os/constants/errno/ERANGE): number
    - const [EROFS](https://bun.com/reference/node/os/constants/errno/EROFS): number
    - const [ESPIPE](https://bun.com/reference/node/os/constants/errno/ESPIPE): number
    - const [ESRCH](https://bun.com/reference/node/os/constants/errno/ESRCH): number
    - const [ESTALE](https://bun.com/reference/node/os/constants/errno/ESTALE): number
    - const [ETIME](https://bun.com/reference/node/os/constants/errno/ETIME): number
    - const [ETIMEDOUT](https://bun.com/reference/node/os/constants/errno/ETIMEDOUT): number
    - const [ETXTBSY](https://bun.com/reference/node/os/constants/errno/ETXTBSY): number
    - const [EWOULDBLOCK](https://bun.com/reference/node/os/constants/errno/EWOULDBLOCK): number
    - const [EXDEV](https://bun.com/reference/node/os/constants/errno/EXDEV): number
    - const [WSA\_E\_CANCELLED](https://bun.com/reference/node/os/constants/errno/WSA_E_CANCELLED): number
    - const [WSA\_E\_NO\_MORE](https://bun.com/reference/node/os/constants/errno/WSA_E_NO_MORE): number
    - const [WSAEACCES](https://bun.com/reference/node/os/constants/errno/WSAEACCES): number
    - const [WSAEADDRINUSE](https://bun.com/reference/node/os/constants/errno/WSAEADDRINUSE): number
    - const [WSAEADDRNOTAVAIL](https://bun.com/reference/node/os/constants/errno/WSAEADDRNOTAVAIL): number
    - const [WSAEAFNOSUPPORT](https://bun.com/reference/node/os/constants/errno/WSAEAFNOSUPPORT): number
    - const [WSAEALREADY](https://bun.com/reference/node/os/constants/errno/WSAEALREADY): number
    - const [WSAEBADF](https://bun.com/reference/node/os/constants/errno/WSAEBADF): number
    - const [WSAECANCELLED](https://bun.com/reference/node/os/constants/errno/WSAECANCELLED): number
    - const [WSAECONNABORTED](https://bun.com/reference/node/os/constants/errno/WSAECONNABORTED): number
    - const [WSAECONNREFUSED](https://bun.com/reference/node/os/constants/errno/WSAECONNREFUSED): number
    - const [WSAECONNRESET](https://bun.com/reference/node/os/constants/errno/WSAECONNRESET): number
    - const [WSAEDESTADDRREQ](https://bun.com/reference/node/os/constants/errno/WSAEDESTADDRREQ): number
    - const [WSAEDISCON](https://bun.com/reference/node/os/constants/errno/WSAEDISCON): number
    - const [WSAEDQUOT](https://bun.com/reference/node/os/constants/errno/WSAEDQUOT): number
    - const [WSAEFAULT](https://bun.com/reference/node/os/constants/errno/WSAEFAULT): number
    - const [WSAEHOSTDOWN](https://bun.com/reference/node/os/constants/errno/WSAEHOSTDOWN): number
    - const [WSAEHOSTUNREACH](https://bun.com/reference/node/os/constants/errno/WSAEHOSTUNREACH): number
    - const [WSAEINPROGRESS](https://bun.com/reference/node/os/constants/errno/WSAEINPROGRESS): number
    - const [WSAEINTR](https://bun.com/reference/node/os/constants/errno/WSAEINTR): number
    - const [WSAEINVAL](https://bun.com/reference/node/os/constants/errno/WSAEINVAL): number
    - const [WSAEINVALIDPROCTABLE](https://bun.com/reference/node/os/constants/errno/WSAEINVALIDPROCTABLE): number
    - const [WSAEINVALIDPROVIDER](https://bun.com/reference/node/os/constants/errno/WSAEINVALIDPROVIDER): number
    - const [WSAEISCONN](https://bun.com/reference/node/os/constants/errno/WSAEISCONN): number
    - const [WSAELOOP](https://bun.com/reference/node/os/constants/errno/WSAELOOP): number
    - const [WSAEMFILE](https://bun.com/reference/node/os/constants/errno/WSAEMFILE): number
    - const [WSAEMSGSIZE](https://bun.com/reference/node/os/constants/errno/WSAEMSGSIZE): number
    - const [WSAENAMETOOLONG](https://bun.com/reference/node/os/constants/errno/WSAENAMETOOLONG): number
    - const [WSAENETDOWN](https://bun.com/reference/node/os/constants/errno/WSAENETDOWN): number
    - const [WSAENETRESET](https://bun.com/reference/node/os/constants/errno/WSAENETRESET): number
    - const [WSAENETUNREACH](https://bun.com/reference/node/os/constants/errno/WSAENETUNREACH): number
    - const [WSAENOBUFS](https://bun.com/reference/node/os/constants/errno/WSAENOBUFS): number
    - const [WSAENOMORE](https://bun.com/reference/node/os/constants/errno/WSAENOMORE): number
    - const [WSAENOPROTOOPT](https://bun.com/reference/node/os/constants/errno/WSAENOPROTOOPT): number
    - const [WSAENOTCONN](https://bun.com/reference/node/os/constants/errno/WSAENOTCONN): number
    - const [WSAENOTEMPTY](https://bun.com/reference/node/os/constants/errno/WSAENOTEMPTY): number
    - const [WSAENOTSOCK](https://bun.com/reference/node/os/constants/errno/WSAENOTSOCK): number
    - const [WSAEOPNOTSUPP](https://bun.com/reference/node/os/constants/errno/WSAEOPNOTSUPP): number
    - const [WSAEPFNOSUPPORT](https://bun.com/reference/node/os/constants/errno/WSAEPFNOSUPPORT): number
    - const [WSAEPROCLIM](https://bun.com/reference/node/os/constants/errno/WSAEPROCLIM): number
    - const [WSAEPROTONOSUPPORT](https://bun.com/reference/node/os/constants/errno/WSAEPROTONOSUPPORT): number
    - const [WSAEPROTOTYPE](https://bun.com/reference/node/os/constants/errno/WSAEPROTOTYPE): number
    - const [WSAEPROVIDERFAILEDINIT](https://bun.com/reference/node/os/constants/errno/WSAEPROVIDERFAILEDINIT): number
    - const [WSAEREFUSED](https://bun.com/reference/node/os/constants/errno/WSAEREFUSED): number
    - const [WSAEREMOTE](https://bun.com/reference/node/os/constants/errno/WSAEREMOTE): number
    - const [WSAESHUTDOWN](https://bun.com/reference/node/os/constants/errno/WSAESHUTDOWN): number
    - const [WSAESOCKTNOSUPPORT](https://bun.com/reference/node/os/constants/errno/WSAESOCKTNOSUPPORT): number
    - const [WSAESTALE](https://bun.com/reference/node/os/constants/errno/WSAESTALE): number
    - const [WSAETIMEDOUT](https://bun.com/reference/node/os/constants/errno/WSAETIMEDOUT): number
    - const [WSAETOOMANYREFS](https://bun.com/reference/node/os/constants/errno/WSAETOOMANYREFS): number
    - const [WSAEUSERS](https://bun.com/reference/node/os/constants/errno/WSAEUSERS): number
    - const [WSAEWOULDBLOCK](https://bun.com/reference/node/os/constants/errno/WSAEWOULDBLOCK): number
    - const [WSANOTINITIALISED](https://bun.com/reference/node/os/constants/errno/WSANOTINITIALISED): number
    - const [WSASERVICE\_NOT\_FOUND](https://bun.com/reference/node/os/constants/errno/WSASERVICE_NOT_FOUND): number
    - const [WSASYSCALLFAILURE](https://bun.com/reference/node/os/constants/errno/WSASYSCALLFAILURE): number
    - const [WSASYSNOTREADY](https://bun.com/reference/node/os/constants/errno/WSASYSNOTREADY): number
    - const [WSATYPE\_NOT\_FOUND](https://bun.com/reference/node/os/constants/errno/WSATYPE_NOT_FOUND): number
    - const [WSAVERNOTSUPPORTED](https://bun.com/reference/node/os/constants/errno/WSAVERNOTSUPPORTED): number
  + ### namespace [priority](https://bun.com/reference/node/os/constants/priority)

    - const [PRIORITY\_ABOVE\_NORMAL](https://bun.com/reference/node/os/constants/priority/PRIORITY_ABOVE_NORMAL): number
    - const [PRIORITY\_BELOW\_NORMAL](https://bun.com/reference/node/os/constants/priority/PRIORITY_BELOW_NORMAL): number
    - const [PRIORITY\_HIGH](https://bun.com/reference/node/os/constants/priority/PRIORITY_HIGH): number
    - const [PRIORITY\_HIGHEST](https://bun.com/reference/node/os/constants/priority/PRIORITY_HIGHEST): number
    - const [PRIORITY\_LOW](https://bun.com/reference/node/os/constants/priority/PRIORITY_LOW): number
    - const [PRIORITY\_NORMAL](https://bun.com/reference/node/os/constants/priority/PRIORITY_NORMAL): number
  + ### namespace [signals](https://bun.com/reference/node/os/constants/signals)
  + const [signals](https://bun.com/reference/node/os/constants/signals): [SignalConstants](https://bun.com/reference/node/os/SignalConstants)
  + const [UV\_UDP\_REUSEADDR](https://bun.com/reference/node/os/constants/UV_UDP_REUSEADDR): number
* const [devNull](https://bun.com/reference/node/os/devNull): string
* const [EOL](https://bun.com/reference/node/os/EOL): string

  The operating system-specific end-of-line marker.

  + ```

    ```

    on POSIX
  + ```
    \r
    ```

    on Windows
* function [arch](https://bun.com/reference/node/os/arch)(): Architecture;

  Returns the operating system CPU architecture for which the Node.js binary was compiled. Possible values are `'arm'`, `'arm64'`, `'ia32'`, `'loong64'`, `'mips'`, `'mipsel'`, `'ppc64'`, `'riscv64'`, `'s390x'`, and `'x64'`.

  The return value is equivalent to [process.arch](https://nodejs.org/docs/latest-v24.x/api/process.html#processarch).
* function [availableParallelism](https://bun.com/reference/node/os/availableParallelism)(): number;

  Returns an estimate of the default amount of parallelism a program should use. Always returns a value greater than zero.

  This function is a small wrapper about libuv's [`uv_available_parallelism()`](https://docs.libuv.org/en/v1.x/misc.html#c.uv_available_parallelism).
* function [cpus](https://bun.com/reference/node/os/cpus)(): [CpuInfo](https://bun.com/reference/node/os/CpuInfo)[];

  Returns an array of objects containing information about each logical CPU core. The array will be empty if no CPU information is available, such as if the `/proc` file system is unavailable.

  The properties included on each object include:

  ```
  [
    {
      model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
      speed: 2926,
      times: {
        user: 252020,
        nice: 0,
        sys: 30340,
        idle: 1070356870,
        irq: 0,
      },
    },
    {
      model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
      speed: 2926,
      times: {
        user: 306960,
        nice: 0,
        sys: 26980,
        idle: 1071569080,
        irq: 0,
      },
    },
    {
      model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
      speed: 2926,
      times: {
        user: 248450,
        nice: 0,
        sys: 21750,
        idle: 1070919370,
        irq: 0,
      },
    },
    {
      model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
      speed: 2926,
      times: {
        user: 256880,
        nice: 0,
        sys: 19430,
        idle: 1070905480,
        irq: 20,
      },
    },
  ]
  ```

  `nice` values are POSIX-only. On Windows, the `nice` values of all processors are always 0.

  `os.cpus().length` should not be used to calculate the amount of parallelism available to an application. Use availableParallelism for this purpose.
* function [endianness](https://bun.com/reference/node/os/endianness)(): 'BE' | 'LE';

  Returns a string identifying the endianness of the CPU for which the Node.js binary was compiled.

  Possible values are `'BE'` for big endian and `'LE'` for little endian.
* function [freemem](https://bun.com/reference/node/os/freemem)(): number;

  Returns the amount of free system memory in bytes as an integer.
* function [getPriority](https://bun.com/reference/node/os/getPriority)(

  pid?: number

  ): number;

  Returns the scheduling priority for the process specified by `pid`. If `pid` is not provided or is `0`, the priority of the current process is returned.

  @param pid

  The process ID to retrieve scheduling priority for.
* function [homedir](https://bun.com/reference/node/os/homedir)(): string;

  Returns the string path of the current user's home directory.

  On POSIX, it uses the `$HOME` environment variable if defined. Otherwise it uses the [effective UID](https://en.wikipedia.org/wiki/User_identifier#Effective_user_ID) to look up the user's home directory.

  On Windows, it uses the `USERPROFILE` environment variable if defined. Otherwise it uses the path to the profile directory of the current user.
* function [hostname](https://bun.com/reference/node/os/hostname)(): string;

  Returns the host name of the operating system as a string.
* function [loadavg](https://bun.com/reference/node/os/loadavg)(): number[];

  Returns an array containing the 1, 5, and 15 minute load averages.

  The load average is a measure of system activity calculated by the operating system and expressed as a fractional number.

  The load average is a Unix-specific concept. On Windows, the return value is always `[0, 0, 0]`.
* function [machine](https://bun.com/reference/node/os/machine)(): string;

  Returns the machine type as a string, such as `arm`, `arm64`, `aarch64`, `mips`, `mips64`, `ppc64`, `ppc64le`, `s390x`, `i386`, `i686`, `x86_64`.

  On POSIX systems, the machine type is determined by calling [`uname(3)`](https://linux.die.net/man/3/uname). On Windows, `RtlGetVersion()` is used, and if it is not available, `GetVersionExW()` will be used. See <https://en.wikipedia.org/wiki/Uname#Examples> for more information.
* function [networkInterfaces](https://bun.com/reference/node/os/networkInterfaces)(): Dict<[NetworkInterfaceInfo](https://bun.com/reference/node/os/NetworkInterfaceInfo)[]>;

  Returns an object containing network interfaces that have been assigned a network address.

  Each key on the returned object identifies a network interface. The associated value is an array of objects that each describe an assigned network address.

  The properties available on the assigned network address object include:

  ```
  {
    lo: [
      {
        address: '127.0.0.1',
        netmask: '255.0.0.0',
        family: 'IPv4',
        mac: '00:00:00:00:00:00',
        internal: true,
        cidr: '127.0.0.1/8'
      },
      {
        address: '::1',
        netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
        family: 'IPv6',
        mac: '00:00:00:00:00:00',
        scopeid: 0,
        internal: true,
        cidr: '::1/128'
      }
    ],
    eth0: [
      {
        address: '192.168.1.108',
        netmask: '255.255.255.0',
        family: 'IPv4',
        mac: '01:02:03:0a:0b:0c',
        internal: false,
        cidr: '192.168.1.108/24'
      },
      {
        address: 'fe80::a00:27ff:fe4e:66a1',
        netmask: 'ffff:ffff:ffff:ffff::',
        family: 'IPv6',
        mac: '01:02:03:0a:0b:0c',
        scopeid: 1,
        internal: false,
        cidr: 'fe80::a00:27ff:fe4e:66a1/64'
      }
    ]
  }
  ```
* function [platform](https://bun.com/reference/node/os/platform)(): Platform;

  Returns a string identifying the operating system platform for which the Node.js binary was compiled. The value is set at compile time. Possible values are `'aix'`, `'darwin'`, `'freebsd'`, `'linux'`, `'openbsd'`, `'sunos'`, and `'win32'`.

  The return value is equivalent to `process.platform`.

  The value `'android'` may also be returned if Node.js is built on the Android operating system. [Android support is experimental](https://github.com/nodejs/node/blob/HEAD/BUILDING.md#androidandroid-based-devices-eg-firefox-os).
* function [release](https://bun.com/reference/node/os/release)(): string;

  Returns the operating system as a string.

  On POSIX systems, the operating system release is determined by calling [`uname(3)`](https://linux.die.net/man/3/uname). On Windows, `GetVersionExW()` is used. See <https://en.wikipedia.org/wiki/Uname#Examples> for more information.
* function [setPriority](https://bun.com/reference/node/os/setPriority)(

  priority: number

  ): void;

  Attempts to set the scheduling priority for the process specified by `pid`. If `pid` is not provided or is `0`, the process ID of the current process is used.

  The `priority` input must be an integer between `-20` (high priority) and `19` (low priority). Due to differences between Unix priority levels and Windows priority classes, `priority` is mapped to one of six priority constants in `os.constants.priority`. When retrieving a process priority level, this range mapping may cause the return value to be slightly different on Windows. To avoid confusion, set `priority` to one of the priority constants.

  On Windows, setting priority to `PRIORITY_HIGHEST` requires elevated user privileges. Otherwise the set priority will be silently reduced to `PRIORITY_HIGH`.

  @param priority

  The scheduling priority to assign to the process.

  function [setPriority](https://bun.com/reference/node/os/setPriority)(

  pid: number,

  priority: number

  ): void;

  Attempts to set the scheduling priority for the process specified by `pid`. If `pid` is not provided or is `0`, the process ID of the current process is used.

  The `priority` input must be an integer between `-20` (high priority) and `19` (low priority). Due to differences between Unix priority levels and Windows priority classes, `priority` is mapped to one of six priority constants in `os.constants.priority`. When retrieving a process priority level, this range mapping may cause the return value to be slightly different on Windows. To avoid confusion, set `priority` to one of the priority constants.

  On Windows, setting priority to `PRIORITY_HIGHEST` requires elevated user privileges. Otherwise the set priority will be silently reduced to `PRIORITY_HIGH`.

  @param pid

  The process ID to set scheduling priority for.

  @param priority

  The scheduling priority to assign to the process.
* function [tmpdir](https://bun.com/reference/node/os/tmpdir)(): string;

  Returns the operating system's default directory for temporary files as a string.
* function [totalmem](https://bun.com/reference/node/os/totalmem)(): number;

  Returns the total amount of system memory in bytes as an integer.
* function [type](https://bun.com/reference/node/os/type)(): string;

  Returns the operating system name as returned by [`uname(3)`](https://linux.die.net/man/3/uname). For example, it returns `'Linux'` on Linux, `'Darwin'` on macOS, and `'Windows_NT'` on Windows.

  See <https://en.wikipedia.org/wiki/Uname#Examples> for additional information about the output of running [`uname(3)`](https://linux.die.net/man/3/uname) on various operating systems.
* function [uptime](https://bun.com/reference/node/os/uptime)(): number;

  Returns the system uptime in number of seconds.
* function [userInfo](https://bun.com/reference/node/os/userInfo)(

  options?: [UserInfoOptionsWithStringEncoding](https://bun.com/reference/node/os/UserInfoOptionsWithStringEncoding)

  ): [UserInfo](https://bun.com/reference/node/os/UserInfo)<string>;

  Returns information about the currently effective user. On POSIX platforms, this is typically a subset of the password file. The returned object includes the `username`, `uid`, `gid`, `shell`, and `homedir`. On Windows, the `uid` and `gid` fields are `-1`, and `shell` is `null`.

  The value of `homedir` returned by `os.userInfo()` is provided by the operating system. This differs from the result of `os.homedir()`, which queries environment variables for the home directory before falling back to the operating system response.

  Throws a [`SystemError`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-systemerror) if a user has no `username` or `homedir`.

  function [userInfo](https://bun.com/reference/node/os/userInfo)(

  options: [UserInfoOptionsWithBufferEncoding](https://bun.com/reference/node/os/UserInfoOptionsWithBufferEncoding)

  ): [UserInfo](https://bun.com/reference/node/os/UserInfo)<NonSharedBuffer>;

  Returns information about the currently effective user. On POSIX platforms, this is typically a subset of the password file. The returned object includes the `username`, `uid`, `gid`, `shell`, and `homedir`. On Windows, the `uid` and `gid` fields are `-1`, and `shell` is `null`.

  The value of `homedir` returned by `os.userInfo()` is provided by the operating system. This differs from the result of `os.homedir()`, which queries environment variables for the home directory before falling back to the operating system response.

  Throws a [`SystemError`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-systemerror) if a user has no `username` or `homedir`.

  function [userInfo](https://bun.com/reference/node/os/userInfo)(

  options: [UserInfoOptions](https://bun.com/reference/node/os/UserInfoOptions)

  ): [UserInfo](https://bun.com/reference/node/os/UserInfo)<string | NonSharedBuffer>;

  Returns information about the currently effective user. On POSIX platforms, this is typically a subset of the password file. The returned object includes the `username`, `uid`, `gid`, `shell`, and `homedir`. On Windows, the `uid` and `gid` fields are `-1`, and `shell` is `null`.

  The value of `homedir` returned by `os.userInfo()` is provided by the operating system. This differs from the result of `os.homedir()`, which queries environment variables for the home directory before falling back to the operating system response.

  Throws a [`SystemError`](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-systemerror) if a user has no `username` or `homedir`.
* function [version](https://bun.com/reference/node/os/version)(): string;

  Returns a string identifying the kernel version.

  On POSIX systems, the operating system release is determined by calling [`uname(3)`](https://linux.die.net/man/3/uname). On Windows, `RtlGetVersion()` is used, and if it is not available, `GetVersionExW()` will be used. See <https://en.wikipedia.org/wiki/Uname#Examples> for more information.

## Type definitions

* ### interface [CpuInfo](https://bun.com/reference/node/os/CpuInfo)

  + [model](https://bun.com/reference/node/os/CpuInfo/model): string
  + [speed](https://bun.com/reference/node/os/CpuInfo/speed): number
  + [times](https://bun.com/reference/node/os/CpuInfo/times): { idle: number; irq: number; nice: number; sys: number; user: number }
* ### interface [NetworkInterfaceBase](https://bun.com/reference/node/os/NetworkInterfaceBase)

  + [address](https://bun.com/reference/node/os/NetworkInterfaceBase/address): string
  + [cidr](https://bun.com/reference/node/os/NetworkInterfaceBase/cidr): null | string
  + [internal](https://bun.com/reference/node/os/NetworkInterfaceBase/internal): boolean
  + [mac](https://bun.com/reference/node/os/NetworkInterfaceBase/mac): string
  + [netmask](https://bun.com/reference/node/os/NetworkInterfaceBase/netmask): string
  + [scopeid](https://bun.com/reference/node/os/NetworkInterfaceBase/scopeid)?: number
* ### interface [NetworkInterfaceInfoIPv4](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4)

  + [address](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/address): string
  + [cidr](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/cidr): null | string
  + [family](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/family): 'IPv4'
  + [internal](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/internal): boolean
  + [mac](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/mac): string
  + [netmask](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/netmask): string
  + [scopeid](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4/scopeid)?: number
* ### interface [NetworkInterfaceInfoIPv6](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6)

  + [address](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/address): string
  + [cidr](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/cidr): null | string
  + [family](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/family): 'IPv6'
  + [internal](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/internal): boolean
  + [mac](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/mac): string
  + [netmask](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/netmask): string
  + [scopeid](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6/scopeid): number
* ### interface [UserInfo](https://bun.com/reference/node/os/UserInfo)<T>

  + [gid](https://bun.com/reference/node/os/UserInfo/gid): number
  + [homedir](https://bun.com/reference/node/os/UserInfo/homedir): T
  + [shell](https://bun.com/reference/node/os/UserInfo/shell): null | T
  + [uid](https://bun.com/reference/node/os/UserInfo/uid): number
  + [username](https://bun.com/reference/node/os/UserInfo/username): T
* ### interface [UserInfoOptions](https://bun.com/reference/node/os/UserInfoOptions)

  + [encoding](https://bun.com/reference/node/os/UserInfoOptions/encoding)?: BufferEncoding | 'buffer'
* ### interface [UserInfoOptionsWithBufferEncoding](https://bun.com/reference/node/os/UserInfoOptionsWithBufferEncoding)

  + [encoding](https://bun.com/reference/node/os/UserInfoOptionsWithBufferEncoding/encoding): 'buffer'
* ### interface [UserInfoOptionsWithStringEncoding](https://bun.com/reference/node/os/UserInfoOptionsWithStringEncoding)

  + [encoding](https://bun.com/reference/node/os/UserInfoOptionsWithStringEncoding/encoding)?: BufferEncoding
* type [NetworkInterfaceInfo](https://bun.com/reference/node/os/NetworkInterfaceInfo) = [NetworkInterfaceInfoIPv4](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv4) | [NetworkInterfaceInfoIPv6](https://bun.com/reference/node/os/NetworkInterfaceInfoIPv6)
* type [SignalConstants](https://bun.com/reference/node/os/SignalConstants) = { [K in NodeJS.Signals]: number }