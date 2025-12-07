---
url: https://bun.com/reference/node/http2
title: Node.js http2 module | API Reference | Bun
source_domain: bun.com
---

# Node.js http2 module | API Reference | Bun

Node.js module

# [http2](https://bun.com/reference/node/http2)

The `'node:http2'` module provides an API for HTTP/2 clients and servers, including support for multiplexing streams, HPACK header compression, and server push.

Works in Bun

Client & server are implemented (95.25% of gRPC's test suite passes). Some options, the ALTSVC extension, and server push functionality are missing.

* ### namespace [constants](https://bun.com/reference/node/http2/constants)

  + const [DEFAULT\_SETTINGS\_ENABLE\_PUSH](https://bun.com/reference/node/http2/constants/DEFAULT_SETTINGS_ENABLE_PUSH): number
  + const [DEFAULT\_SETTINGS\_HEADER\_TABLE\_SIZE](https://bun.com/reference/node/http2/constants/DEFAULT_SETTINGS_HEADER_TABLE_SIZE): number
  + const [DEFAULT\_SETTINGS\_INITIAL\_WINDOW\_SIZE](https://bun.com/reference/node/http2/constants/DEFAULT_SETTINGS_INITIAL_WINDOW_SIZE): number
  + const [DEFAULT\_SETTINGS\_MAX\_FRAME\_SIZE](https://bun.com/reference/node/http2/constants/DEFAULT_SETTINGS_MAX_FRAME_SIZE): number
  + const [HTTP\_STATUS\_ACCEPTED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_ACCEPTED): number
  + const [HTTP\_STATUS\_ALREADY\_REPORTED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_ALREADY_REPORTED): number
  + const [HTTP\_STATUS\_BAD\_GATEWAY](https://bun.com/reference/node/http2/constants/HTTP_STATUS_BAD_GATEWAY): number
  + const [HTTP\_STATUS\_BAD\_REQUEST](https://bun.com/reference/node/http2/constants/HTTP_STATUS_BAD_REQUEST): number
  + const [HTTP\_STATUS\_BANDWIDTH\_LIMIT\_EXCEEDED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_BANDWIDTH_LIMIT_EXCEEDED): number
  + const [HTTP\_STATUS\_CONFLICT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_CONFLICT): number
  + const [HTTP\_STATUS\_CONTINUE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_CONTINUE): number
  + const [HTTP\_STATUS\_CREATED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_CREATED): number
  + const [HTTP\_STATUS\_EXPECTATION\_FAILED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_EXPECTATION_FAILED): number
  + const [HTTP\_STATUS\_FAILED\_DEPENDENCY](https://bun.com/reference/node/http2/constants/HTTP_STATUS_FAILED_DEPENDENCY): number
  + const [HTTP\_STATUS\_FORBIDDEN](https://bun.com/reference/node/http2/constants/HTTP_STATUS_FORBIDDEN): number
  + const [HTTP\_STATUS\_FOUND](https://bun.com/reference/node/http2/constants/HTTP_STATUS_FOUND): number
  + const [HTTP\_STATUS\_GATEWAY\_TIMEOUT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_GATEWAY_TIMEOUT): number
  + const [HTTP\_STATUS\_GONE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_GONE): number
  + const [HTTP\_STATUS\_HTTP\_VERSION\_NOT\_SUPPORTED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_HTTP_VERSION_NOT_SUPPORTED): number
  + const [HTTP\_STATUS\_IM\_USED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_IM_USED): number
  + const [HTTP\_STATUS\_INSUFFICIENT\_STORAGE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_INSUFFICIENT_STORAGE): number
  + const [HTTP\_STATUS\_INTERNAL\_SERVER\_ERROR](https://bun.com/reference/node/http2/constants/HTTP_STATUS_INTERNAL_SERVER_ERROR): number
  + const [HTTP\_STATUS\_LENGTH\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_LENGTH_REQUIRED): number
  + const [HTTP\_STATUS\_LOCKED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_LOCKED): number
  + const [HTTP\_STATUS\_LOOP\_DETECTED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_LOOP_DETECTED): number
  + const [HTTP\_STATUS\_METHOD\_NOT\_ALLOWED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_METHOD_NOT_ALLOWED): number
  + const [HTTP\_STATUS\_MISDIRECTED\_REQUEST](https://bun.com/reference/node/http2/constants/HTTP_STATUS_MISDIRECTED_REQUEST): number
  + const [HTTP\_STATUS\_MOVED\_PERMANENTLY](https://bun.com/reference/node/http2/constants/HTTP_STATUS_MOVED_PERMANENTLY): number
  + const [HTTP\_STATUS\_MULTI\_STATUS](https://bun.com/reference/node/http2/constants/HTTP_STATUS_MULTI_STATUS): number
  + const [HTTP\_STATUS\_MULTIPLE\_CHOICES](https://bun.com/reference/node/http2/constants/HTTP_STATUS_MULTIPLE_CHOICES): number
  + const [HTTP\_STATUS\_NETWORK\_AUTHENTICATION\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NETWORK_AUTHENTICATION_REQUIRED): number
  + const [HTTP\_STATUS\_NO\_CONTENT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NO_CONTENT): number
  + const [HTTP\_STATUS\_NON\_AUTHORITATIVE\_INFORMATION](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NON_AUTHORITATIVE_INFORMATION): number
  + const [HTTP\_STATUS\_NOT\_ACCEPTABLE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NOT_ACCEPTABLE): number
  + const [HTTP\_STATUS\_NOT\_EXTENDED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NOT_EXTENDED): number
  + const [HTTP\_STATUS\_NOT\_FOUND](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NOT_FOUND): number
  + const [HTTP\_STATUS\_NOT\_IMPLEMENTED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NOT_IMPLEMENTED): number
  + const [HTTP\_STATUS\_NOT\_MODIFIED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_NOT_MODIFIED): number
  + const [HTTP\_STATUS\_OK](https://bun.com/reference/node/http2/constants/HTTP_STATUS_OK): number
  + const [HTTP\_STATUS\_PARTIAL\_CONTENT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PARTIAL_CONTENT): number
  + const [HTTP\_STATUS\_PAYLOAD\_TOO\_LARGE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PAYLOAD_TOO_LARGE): number
  + const [HTTP\_STATUS\_PAYMENT\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PAYMENT_REQUIRED): number
  + const [HTTP\_STATUS\_PERMANENT\_REDIRECT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PERMANENT_REDIRECT): number
  + const [HTTP\_STATUS\_PRECONDITION\_FAILED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PRECONDITION_FAILED): number
  + const [HTTP\_STATUS\_PRECONDITION\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PRECONDITION_REQUIRED): number
  + const [HTTP\_STATUS\_PROCESSING](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PROCESSING): number
  + const [HTTP\_STATUS\_PROXY\_AUTHENTICATION\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_PROXY_AUTHENTICATION_REQUIRED): number
  + const [HTTP\_STATUS\_RANGE\_NOT\_SATISFIABLE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_RANGE_NOT_SATISFIABLE): number
  + const [HTTP\_STATUS\_REQUEST\_HEADER\_FIELDS\_TOO\_LARGE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_REQUEST_HEADER_FIELDS_TOO_LARGE): number
  + const [HTTP\_STATUS\_REQUEST\_TIMEOUT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_REQUEST_TIMEOUT): number
  + const [HTTP\_STATUS\_RESET\_CONTENT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_RESET_CONTENT): number
  + const [HTTP\_STATUS\_SEE\_OTHER](https://bun.com/reference/node/http2/constants/HTTP_STATUS_SEE_OTHER): number
  + const [HTTP\_STATUS\_SERVICE\_UNAVAILABLE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_SERVICE_UNAVAILABLE): number
  + const [HTTP\_STATUS\_SWITCHING\_PROTOCOLS](https://bun.com/reference/node/http2/constants/HTTP_STATUS_SWITCHING_PROTOCOLS): number
  + const [HTTP\_STATUS\_TEAPOT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_TEAPOT): number
  + const [HTTP\_STATUS\_TEMPORARY\_REDIRECT](https://bun.com/reference/node/http2/constants/HTTP_STATUS_TEMPORARY_REDIRECT): number
  + const [HTTP\_STATUS\_TOO\_MANY\_REQUESTS](https://bun.com/reference/node/http2/constants/HTTP_STATUS_TOO_MANY_REQUESTS): number
  + const [HTTP\_STATUS\_UNAUTHORIZED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UNAUTHORIZED): number
  + const [HTTP\_STATUS\_UNAVAILABLE\_FOR\_LEGAL\_REASONS](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UNAVAILABLE_FOR_LEGAL_REASONS): number
  + const [HTTP\_STATUS\_UNORDERED\_COLLECTION](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UNORDERED_COLLECTION): number
  + const [HTTP\_STATUS\_UNPROCESSABLE\_ENTITY](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UNPROCESSABLE_ENTITY): number
  + const [HTTP\_STATUS\_UNSUPPORTED\_MEDIA\_TYPE](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UNSUPPORTED_MEDIA_TYPE): number
  + const [HTTP\_STATUS\_UPGRADE\_REQUIRED](https://bun.com/reference/node/http2/constants/HTTP_STATUS_UPGRADE_REQUIRED): number
  + const [HTTP\_STATUS\_URI\_TOO\_LONG](https://bun.com/reference/node/http2/constants/HTTP_STATUS_URI_TOO_LONG): number
  + const [HTTP\_STATUS\_USE\_PROXY](https://bun.com/reference/node/http2/constants/HTTP_STATUS_USE_PROXY): number
  + const [HTTP\_STATUS\_VARIANT\_ALSO\_NEGOTIATES](https://bun.com/reference/node/http2/constants/HTTP_STATUS_VARIANT_ALSO_NEGOTIATES): number
  + const [HTTP2\_HEADER\_ACCEPT](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCEPT): string
  + const [HTTP2\_HEADER\_ACCEPT\_CHARSET](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCEPT_CHARSET): string
  + const [HTTP2\_HEADER\_ACCEPT\_ENCODING](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCEPT_ENCODING): string
  + const [HTTP2\_HEADER\_ACCEPT\_LANGUAGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCEPT_LANGUAGE): string
  + const [HTTP2\_HEADER\_ACCEPT\_RANGES](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCEPT_RANGES): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_ALLOW\_CREDENTIALS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_ALLOW_CREDENTIALS): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_ALLOW\_HEADERS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_ALLOW_HEADERS): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_ALLOW\_METHODS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_ALLOW_METHODS): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_ALLOW\_ORIGIN](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_ALLOW_ORIGIN): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_EXPOSE\_HEADERS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_EXPOSE_HEADERS): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_REQUEST\_HEADERS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_REQUEST_HEADERS): string
  + const [HTTP2\_HEADER\_ACCESS\_CONTROL\_REQUEST\_METHOD](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ACCESS_CONTROL_REQUEST_METHOD): string
  + const [HTTP2\_HEADER\_AGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_AGE): string
  + const [HTTP2\_HEADER\_ALLOW](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ALLOW): string
  + const [HTTP2\_HEADER\_AUTHORITY](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_AUTHORITY): string
  + const [HTTP2\_HEADER\_AUTHORIZATION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_AUTHORIZATION): string
  + const [HTTP2\_HEADER\_CACHE\_CONTROL](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CACHE_CONTROL): string
  + const [HTTP2\_HEADER\_CONNECTION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONNECTION): string
  + const [HTTP2\_HEADER\_CONTENT\_DISPOSITION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_DISPOSITION): string
  + const [HTTP2\_HEADER\_CONTENT\_ENCODING](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_ENCODING): string
  + const [HTTP2\_HEADER\_CONTENT\_LANGUAGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_LANGUAGE): string
  + const [HTTP2\_HEADER\_CONTENT\_LENGTH](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_LENGTH): string
  + const [HTTP2\_HEADER\_CONTENT\_LOCATION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_LOCATION): string
  + const [HTTP2\_HEADER\_CONTENT\_MD5](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_MD5): string
  + const [HTTP2\_HEADER\_CONTENT\_RANGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_RANGE): string
  + const [HTTP2\_HEADER\_CONTENT\_TYPE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_CONTENT_TYPE): string
  + const [HTTP2\_HEADER\_COOKIE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_COOKIE): string
  + const [HTTP2\_HEADER\_DATE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_DATE): string
  + const [HTTP2\_HEADER\_ETAG](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_ETAG): string
  + const [HTTP2\_HEADER\_EXPECT](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_EXPECT): string
  + const [HTTP2\_HEADER\_EXPIRES](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_EXPIRES): string
  + const [HTTP2\_HEADER\_FROM](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_FROM): string
  + const [HTTP2\_HEADER\_HOST](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_HOST): string
  + const [HTTP2\_HEADER\_HTTP2\_SETTINGS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_HTTP2_SETTINGS): string
  + const [HTTP2\_HEADER\_IF\_MATCH](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_IF_MATCH): string
  + const [HTTP2\_HEADER\_IF\_MODIFIED\_SINCE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_IF_MODIFIED_SINCE): string
  + const [HTTP2\_HEADER\_IF\_NONE\_MATCH](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_IF_NONE_MATCH): string
  + const [HTTP2\_HEADER\_IF\_RANGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_IF_RANGE): string
  + const [HTTP2\_HEADER\_IF\_UNMODIFIED\_SINCE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_IF_UNMODIFIED_SINCE): string
  + const [HTTP2\_HEADER\_KEEP\_ALIVE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_KEEP_ALIVE): string
  + const [HTTP2\_HEADER\_LAST\_MODIFIED](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_LAST_MODIFIED): string
  + const [HTTP2\_HEADER\_LINK](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_LINK): string
  + const [HTTP2\_HEADER\_LOCATION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_LOCATION): string
  + const [HTTP2\_HEADER\_MAX\_FORWARDS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_MAX_FORWARDS): string
  + const [HTTP2\_HEADER\_METHOD](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_METHOD): string
  + const [HTTP2\_HEADER\_PATH](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_PATH): string
  + const [HTTP2\_HEADER\_PREFER](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_PREFER): string
  + const [HTTP2\_HEADER\_PROXY\_AUTHENTICATE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_PROXY_AUTHENTICATE): string
  + const [HTTP2\_HEADER\_PROXY\_AUTHORIZATION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_PROXY_AUTHORIZATION): string
  + const [HTTP2\_HEADER\_PROXY\_CONNECTION](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_PROXY_CONNECTION): string
  + const [HTTP2\_HEADER\_RANGE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_RANGE): string
  + const [HTTP2\_HEADER\_REFERER](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_REFERER): string
  + const [HTTP2\_HEADER\_REFRESH](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_REFRESH): string
  + const [HTTP2\_HEADER\_RETRY\_AFTER](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_RETRY_AFTER): string
  + const [HTTP2\_HEADER\_SCHEME](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_SCHEME): string
  + const [HTTP2\_HEADER\_SERVER](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_SERVER): string
  + const [HTTP2\_HEADER\_SET\_COOKIE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_SET_COOKIE): string
  + const [HTTP2\_HEADER\_STATUS](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_STATUS): string
  + const [HTTP2\_HEADER\_STRICT\_TRANSPORT\_SECURITY](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_STRICT_TRANSPORT_SECURITY): string
  + const [HTTP2\_HEADER\_TE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_TE): string
  + const [HTTP2\_HEADER\_TRANSFER\_ENCODING](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_TRANSFER_ENCODING): string
  + const [HTTP2\_HEADER\_UPGRADE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_UPGRADE): string
  + const [HTTP2\_HEADER\_USER\_AGENT](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_USER_AGENT): string
  + const [HTTP2\_HEADER\_VARY](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_VARY): string
  + const [HTTP2\_HEADER\_VIA](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_VIA): string
  + const [HTTP2\_HEADER\_WWW\_AUTHENTICATE](https://bun.com/reference/node/http2/constants/HTTP2_HEADER_WWW_AUTHENTICATE): string
  + const [HTTP2\_METHOD\_ACL](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_ACL): string
  + const [HTTP2\_METHOD\_BASELINE\_CONTROL](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_BASELINE_CONTROL): string
  + const [HTTP2\_METHOD\_BIND](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_BIND): string
  + const [HTTP2\_METHOD\_CHECKIN](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_CHECKIN): string
  + const [HTTP2\_METHOD\_CHECKOUT](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_CHECKOUT): string
  + const [HTTP2\_METHOD\_CONNECT](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_CONNECT): string
  + const [HTTP2\_METHOD\_COPY](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_COPY): string
  + const [HTTP2\_METHOD\_DELETE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_DELETE): string
  + const [HTTP2\_METHOD\_GET](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_GET): string
  + const [HTTP2\_METHOD\_HEAD](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_HEAD): string
  + const [HTTP2\_METHOD\_LABEL](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_LABEL): string
  + const [HTTP2\_METHOD\_LINK](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_LINK): string
  + const [HTTP2\_METHOD\_LOCK](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_LOCK): string
  + const [HTTP2\_METHOD\_MERGE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MERGE): string
  + const [HTTP2\_METHOD\_MKACTIVITY](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MKACTIVITY): string
  + const [HTTP2\_METHOD\_MKCALENDAR](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MKCALENDAR): string
  + const [HTTP2\_METHOD\_MKCOL](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MKCOL): string
  + const [HTTP2\_METHOD\_MKREDIRECTREF](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MKREDIRECTREF): string
  + const [HTTP2\_METHOD\_MKWORKSPACE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MKWORKSPACE): string
  + const [HTTP2\_METHOD\_MOVE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_MOVE): string
  + const [HTTP2\_METHOD\_OPTIONS](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_OPTIONS): string
  + const [HTTP2\_METHOD\_ORDERPATCH](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_ORDERPATCH): string
  + const [HTTP2\_METHOD\_PATCH](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_PATCH): string
  + const [HTTP2\_METHOD\_POST](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_POST): string
  + const [HTTP2\_METHOD\_PRI](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_PRI): string
  + const [HTTP2\_METHOD\_PROPFIND](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_PROPFIND): string
  + const [HTTP2\_METHOD\_PROPPATCH](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_PROPPATCH): string
  + const [HTTP2\_METHOD\_PUT](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_PUT): string
  + const [HTTP2\_METHOD\_REBIND](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_REBIND): string
  + const [HTTP2\_METHOD\_REPORT](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_REPORT): string
  + const [HTTP2\_METHOD\_SEARCH](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_SEARCH): string
  + const [HTTP2\_METHOD\_TRACE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_TRACE): string
  + const [HTTP2\_METHOD\_UNBIND](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UNBIND): string
  + const [HTTP2\_METHOD\_UNCHECKOUT](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UNCHECKOUT): string
  + const [HTTP2\_METHOD\_UNLINK](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UNLINK): string
  + const [HTTP2\_METHOD\_UNLOCK](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UNLOCK): string
  + const [HTTP2\_METHOD\_UPDATE](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UPDATE): string
  + const [HTTP2\_METHOD\_UPDATEREDIRECTREF](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_UPDATEREDIRECTREF): string
  + const [HTTP2\_METHOD\_VERSION\_CONTROL](https://bun.com/reference/node/http2/constants/HTTP2_METHOD_VERSION_CONTROL): string
  + const [MAX\_INITIAL\_WINDOW\_SIZE](https://bun.com/reference/node/http2/constants/MAX_INITIAL_WINDOW_SIZE): number
  + const [MAX\_MAX\_FRAME\_SIZE](https://bun.com/reference/node/http2/constants/MAX_MAX_FRAME_SIZE): number
  + const [MIN\_MAX\_FRAME\_SIZE](https://bun.com/reference/node/http2/constants/MIN_MAX_FRAME_SIZE): number
  + const [NGHTTP2\_CANCEL](https://bun.com/reference/node/http2/constants/NGHTTP2_CANCEL): number
  + const [NGHTTP2\_COMPRESSION\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_COMPRESSION_ERROR): number
  + const [NGHTTP2\_CONNECT\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_CONNECT_ERROR): number
  + const [NGHTTP2\_DEFAULT\_WEIGHT](https://bun.com/reference/node/http2/constants/NGHTTP2_DEFAULT_WEIGHT): number
  + const [NGHTTP2\_ENHANCE\_YOUR\_CALM](https://bun.com/reference/node/http2/constants/NGHTTP2_ENHANCE_YOUR_CALM): number
  + const [NGHTTP2\_ERR\_FRAME\_SIZE\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_ERR_FRAME_SIZE_ERROR): number
  + const [NGHTTP2\_FLAG\_ACK](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_ACK): number
  + const [NGHTTP2\_FLAG\_END\_HEADERS](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_END_HEADERS): number
  + const [NGHTTP2\_FLAG\_END\_STREAM](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_END_STREAM): number
  + const [NGHTTP2\_FLAG\_NONE](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_NONE): number
  + const [NGHTTP2\_FLAG\_PADDED](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_PADDED): number
  + const [NGHTTP2\_FLAG\_PRIORITY](https://bun.com/reference/node/http2/constants/NGHTTP2_FLAG_PRIORITY): number
  + const [NGHTTP2\_FLOW\_CONTROL\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_FLOW_CONTROL_ERROR): number
  + const [NGHTTP2\_FRAME\_SIZE\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_FRAME_SIZE_ERROR): number
  + const [NGHTTP2\_HTTP\_1\_1\_REQUIRED](https://bun.com/reference/node/http2/constants/NGHTTP2_HTTP_1_1_REQUIRED): number
  + const [NGHTTP2\_INADEQUATE\_SECURITY](https://bun.com/reference/node/http2/constants/NGHTTP2_INADEQUATE_SECURITY): number
  + const [NGHTTP2\_INTERNAL\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_INTERNAL_ERROR): number
  + const [NGHTTP2\_NO\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_NO_ERROR): number
  + const [NGHTTP2\_PROTOCOL\_ERROR](https://bun.com/reference/node/http2/constants/NGHTTP2_PROTOCOL_ERROR): number
  + const [NGHTTP2\_REFUSED\_STREAM](https://bun.com/reference/node/http2/constants/NGHTTP2_REFUSED_STREAM): number
  + const [NGHTTP2\_SESSION\_CLIENT](https://bun.com/reference/node/http2/constants/NGHTTP2_SESSION_CLIENT): number
  + const [NGHTTP2\_SESSION\_SERVER](https://bun.com/reference/node/http2/constants/NGHTTP2_SESSION_SERVER): number
  + const [NGHTTP2\_SETTINGS\_ENABLE\_PUSH](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_ENABLE_PUSH): number
  + const [NGHTTP2\_SETTINGS\_HEADER\_TABLE\_SIZE](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_HEADER_TABLE_SIZE): number
  + const [NGHTTP2\_SETTINGS\_INITIAL\_WINDOW\_SIZE](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_INITIAL_WINDOW_SIZE): number
  + const [NGHTTP2\_SETTINGS\_MAX\_CONCURRENT\_STREAMS](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_MAX_CONCURRENT_STREAMS): number
  + const [NGHTTP2\_SETTINGS\_MAX\_FRAME\_SIZE](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_MAX_FRAME_SIZE): number
  + const [NGHTTP2\_SETTINGS\_MAX\_HEADER\_LIST\_SIZE](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_MAX_HEADER_LIST_SIZE): number
  + const [NGHTTP2\_SETTINGS\_TIMEOUT](https://bun.com/reference/node/http2/constants/NGHTTP2_SETTINGS_TIMEOUT): number
  + const [NGHTTP2\_STREAM\_CLOSED](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_CLOSED): number
  + const [NGHTTP2\_STREAM\_STATE\_CLOSED](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_CLOSED): number
  + const [NGHTTP2\_STREAM\_STATE\_HALF\_CLOSED\_LOCAL](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_HALF_CLOSED_LOCAL): number
  + const [NGHTTP2\_STREAM\_STATE\_HALF\_CLOSED\_REMOTE](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_HALF_CLOSED_REMOTE): number
  + const [NGHTTP2\_STREAM\_STATE\_IDLE](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_IDLE): number
  + const [NGHTTP2\_STREAM\_STATE\_OPEN](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_OPEN): number
  + const [NGHTTP2\_STREAM\_STATE\_RESERVED\_LOCAL](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_RESERVED_LOCAL): number
  + const [NGHTTP2\_STREAM\_STATE\_RESERVED\_REMOTE](https://bun.com/reference/node/http2/constants/NGHTTP2_STREAM_STATE_RESERVED_REMOTE): number
  + const [PADDING\_STRATEGY\_CALLBACK](https://bun.com/reference/node/http2/constants/PADDING_STRATEGY_CALLBACK): number
  + const [PADDING\_STRATEGY\_MAX](https://bun.com/reference/node/http2/constants/PADDING_STRATEGY_MAX): number
  + const [PADDING\_STRATEGY\_NONE](https://bun.com/reference/node/http2/constants/PADDING_STRATEGY_NONE): number
* ### class [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest)

  A `Http2ServerRequest` object is created by Server or SecureServer and passed as the first argument to the `'request'` event. It may be used to access a request status, headers, and data.

  + readonly [aborted](https://bun.com/reference/node/http2/Http2ServerRequest/aborted): boolean

    The `request.aborted` property will be `true` if the request has been aborted.
  + readonly [authority](https://bun.com/reference/node/http2/Http2ServerRequest/authority): string

    The request authority pseudo header field. Because HTTP/2 allows requests to set either `:authority` or `host`, this value is derived from `req.headers[':authority']` if present. Otherwise, it is derived from `req.headers['host']`.
  + readonly [closed](https://bun.com/reference/node/http2/Http2ServerRequest/closed): boolean

    Is `true` after `'close'` has been emitted.
  + readonly [complete](https://bun.com/reference/node/http2/Http2ServerRequest/complete): boolean

    The `request.complete` property will be `true` if the request has been completed, aborted, or destroyed.
  + [destroyed](https://bun.com/reference/node/http2/Http2ServerRequest/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http2/Http2ServerRequest/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headers](https://bun.com/reference/node/http2/Http2ServerRequest/headers): [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders)

    The request/response headers object.

    Key-value pairs of header names and values. Header names are lower-cased.

    ```
    // Prints something like:
    //
    // { 'user-agent': 'curl/7.22.0',
    //   host: '127.0.0.1:8000',
    //   accept: '*' }
    console.log(request.headers);
    ```

    See `HTTP/2 Headers Object`.

    In HTTP/2, the request path, host name, protocol, and method are represented as special headers prefixed with the `:` character (e.g. `':path'`). These special headers will be included in the `request.headers` object. Care must be taken not to inadvertently modify these special headers or errors may occur. For instance, removing all headers from the request will cause errors to occur:

    ```
    removeAllHeaders(request.headers);
    assert(request.url);   // Fails because the :path header has been removed
    ```
  + readonly [httpVersion](https://bun.com/reference/node/http2/Http2ServerRequest/httpVersion): string

    In case of server request, the HTTP version sent by the client. In the case of client response, the HTTP version of the connected-to server. Returns `'2.0'`.

    Also `message.httpVersionMajor` is the first integer and `message.httpVersionMinor` is the second.
  + readonly [httpVersionMajor](https://bun.com/reference/node/http2/Http2ServerRequest/httpVersionMajor): number
  + readonly [httpVersionMinor](https://bun.com/reference/node/http2/Http2ServerRequest/httpVersionMinor): number
  + readonly [method](https://bun.com/reference/node/http2/Http2ServerRequest/method): string

    The request method as a string. Read-only. Examples: `'GET'`, `'DELETE'`.
  + readonly [rawHeaders](https://bun.com/reference/node/http2/Http2ServerRequest/rawHeaders): string[]

    The raw request/response headers list exactly as they were received.

    The keys and values are in the same list. It is *not* a list of tuples. So, the even-numbered offsets are key values, and the odd-numbered offsets are the associated values.

    Header names are not lowercased, and duplicates are not merged.

    ```
    // Prints something like:
    //
    // [ 'user-agent',
    //   'this is invalid because there can be only one',
    //   'User-Agent',
    //   'curl/7.22.0',
    //   'Host',
    //   '127.0.0.1:8000',
    //   'ACCEPT',
    //   '*' ]
    console.log(request.rawHeaders);
    ```
  + readonly [rawTrailers](https://bun.com/reference/node/http2/Http2ServerRequest/rawTrailers): string[]

    The raw request/response trailer keys and values exactly as they were received. Only populated at the `'end'` event.
  + [readable](https://bun.com/reference/node/http2/Http2ServerRequest/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/http2/Http2ServerRequest/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/http2/Http2ServerRequest/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/http2/Http2ServerRequest/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/http2/Http2ServerRequest/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/http2/Http2ServerRequest/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/http2/Http2ServerRequest/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/http2/Http2ServerRequest/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/http2/Http2ServerRequest/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [scheme](https://bun.com/reference/node/http2/Http2ServerRequest/scheme): string

    The request scheme pseudo header field indicating the scheme portion of the target URL.
  + readonly [socket](https://bun.com/reference/node/http2/Http2ServerRequest/socket): [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    Returns a `Proxy` object that acts as a `net.Socket` (or `tls.TLSSocket`) but applies getters, setters, and methods based on HTTP/2 logic.

    `destroyed`, `readable`, and `writable` properties will be retrieved from and set on `request.stream`.

    `destroy`, `emit`, `end`, `on` and `once` methods will be called on `request.stream`.

    `setTimeout` method will be called on `request.stream.session`.

    `pause`, `read`, `resume`, and `write` will throw an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See `Http2Session and Sockets` for more information.

    All other interactions will be routed directly to the socket. With TLS support, use `request.socket.getPeerCertificate()` to obtain the client's authentication details.
  + readonly [stream](https://bun.com/reference/node/http2/Http2ServerRequest/stream): [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream)

    The `Http2Stream` object backing the request.
  + readonly [trailers](https://bun.com/reference/node/http2/Http2ServerRequest/trailers): [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders)

    The request/response trailers object. Only populated at the `'end'` event.
  + [url](https://bun.com/reference/node/http2/Http2ServerRequest/url): string

    Request URL string. This contains only the URL that is present in the actual HTTP request. If the request is:

    ```
    GET /status?name=ryan HTTP/1.1
    Accept: text/plain
    ```

    Then `request.url` will be:

    ```
    '/status?name=ryan'
    ```

    To parse the url into its parts, `new URL()` can be used:

    ```
    $ node
    > new URL('/status?name=ryan', 'http://example.com')
    URL {
      href: 'http://example.com/status?name=ryan',
      origin: 'http://example.com',
      protocol: 'http:',
      username: '',
      password: '',
      host: 'example.com',
      hostname: 'example.com',
      port: '',
      pathname: '/status',
      search: '?name=ryan',
      searchParams: URLSearchParams { 'name' => 'ryan' },
      hash: ''
    }
    ```
  + static [captureRejections](https://bun.com/reference/node/http2/Http2ServerRequest/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http2/Http2ServerRequest/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http2/Http2ServerRequest/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/http2/Http2ServerRequest/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http2/Http2ServerRequest/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http2/Http2ServerRequest/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/http2/Http2ServerRequest/_read)(

    size: number

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/Http2ServerRequest/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/http2/Http2ServerRequest/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2ServerRequest/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'aborted',

    listener: (hadError: boolean, code: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http2/Http2ServerRequest/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume
  + [asIndexedPairs](https://bun.com/reference/node/http2/Http2ServerRequest/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [compose](https://bun.com/reference/node/http2/Http2ServerRequest/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [destroy](https://bun.com/reference/node/http2/Http2ServerRequest/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/http2/Http2ServerRequest/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'aborted',

    hadError: boolean,

    code: number

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'data',

    chunk: string | NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerRequest/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/http2/Http2ServerRequest/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/http2/Http2ServerRequest/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/http2/Http2ServerRequest/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/http2/Http2ServerRequest/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/http2/Http2ServerRequest/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/http2/Http2ServerRequest/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/http2/Http2ServerRequest/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2ServerRequest/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/http2/Http2ServerRequest/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/http2/Http2ServerRequest/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/http2/Http2ServerRequest/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2ServerRequest/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/http2/Http2ServerRequest/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/http2/Http2ServerRequest/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'aborted',

    listener: (hadError: boolean, code: number) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'aborted',

    listener: (hadError: boolean, code: number) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/http2/Http2ServerRequest/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/http2/Http2ServerRequest/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'aborted',

    listener: (hadError: boolean, code: number) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'aborted',

    listener: (hadError: boolean, code: number) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerRequest/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/http2/Http2ServerRequest/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/http2/Http2ServerRequest/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/http2/Http2ServerRequest/read)(

    size?: number

    ): null | string | NonSharedBuffer;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/http2/Http2ServerRequest/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/http2/Http2ServerRequest/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2ServerRequest/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerRequest/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/http2/Http2ServerRequest/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setEncoding](https://bun.com/reference/node/http2/Http2ServerRequest/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2ServerRequest/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/Http2ServerRequest/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    Sets the `Http2Stream`'s timeout value to `msecs`. If a callback is provided, then it is added as a listener on the `'timeout'` event on the response object.

    If no `'timeout'` listener is added to the request, the response, or the server, then `Http2Stream`s are destroyed when they time out. If a handler is assigned to the request, the response, or the server's `'timeout'`events, timed out sockets must be handled explicitly.
  + [some](https://bun.com/reference/node/http2/Http2ServerRequest/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/http2/Http2ServerRequest/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/http2/Http2ServerRequest/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [unpipe](https://bun.com/reference/node/http2/Http2ServerRequest/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/http2/Http2ServerRequest/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/http2/Http2ServerRequest/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + static [addAbortListener](https://bun.com/reference/node/http2/Http2ServerRequest/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [from](https://bun.com/reference/node/http2/Http2ServerRequest/from)(

    iterable: Iterable<any, any, any> | AsyncIterable<any, any, any>,

    options?: [ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating Readable Streams out of iterators.

    @param iterable

    Object implementing the `Symbol.asyncIterator` or `Symbol.iterator` iterable protocol. Emits an 'error' event if a null value is passed.

    @param options

    Options provided to `new stream.Readable([options])`. By default, `Readable.from()` will set `options.objectMode` to `true`, unless this is explicitly opted out by setting `options.objectMode` to `false`.
  + static [fromWeb](https://bun.com/reference/node/http2/Http2ServerRequest/fromWeb)(

    readableStream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream),

    options?: Pick<[ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>, 'signal' | 'encoding' | 'highWaterMark' | 'objectMode'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating a `Readable` from a web `ReadableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http2/Http2ServerRequest/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/http2/Http2ServerRequest/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [isDisturbed](https://bun.com/reference/node/http2/Http2ServerRequest/isDisturbed)(

    stream: [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream

    ): boolean;

    Returns whether the stream has been read from or cancelled.
  + static [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/http2/Http2ServerRequest/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/http2/Http2ServerRequest/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/http2/Http2ServerRequest/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
  + static [toWeb](https://bun.com/reference/node/http2/Http2ServerRequest/toWeb)(

    streamReadable: [Readable](https://bun.com/reference/node/stream/default/Readable),

    options?: { strategy: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<any> }

    ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    A utility method for creating a web `ReadableStream` from a `Readable`.
* ### class [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)<Request extends [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest)>

  This object is created internally by an HTTP server, not by the user. It is passed as the second parameter to the `'request'` event.

  + readonly [closed](https://bun.com/reference/node/http2/Http2ServerResponse/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/http2/Http2ServerResponse/destroyed): boolean

    Is `true` after `writable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http2/Http2ServerResponse/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headersSent](https://bun.com/reference/node/http2/Http2ServerResponse/headersSent): boolean

    True if headers were sent, false otherwise (read-only).
  + readonly [req](https://bun.com/reference/node/http2/Http2ServerResponse/req): Request

    A reference to the original HTTP2 `request` object.
  + [sendDate](https://bun.com/reference/node/http2/Http2ServerResponse/sendDate): boolean

    When true, the Date header will be automatically generated and sent in the response if it is not already present in the headers. Defaults to true.

    This should only be disabled for testing; HTTP requires the Date header in responses.
  + readonly [socket](https://bun.com/reference/node/http2/Http2ServerResponse/socket): [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    Returns a `Proxy` object that acts as a `net.Socket` (or `tls.TLSSocket`) but applies getters, setters, and methods based on HTTP/2 logic.

    `destroyed`, `readable`, and `writable` properties will be retrieved from and set on `response.stream`.

    `destroy`, `emit`, `end`, `on` and `once` methods will be called on `response.stream`.

    `setTimeout` method will be called on `response.stream.session`.

    `pause`, `read`, `resume`, and `write` will throw an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See `Http2Session and Sockets` for more information.

    All other interactions will be routed directly to the socket.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer((req, res) => {
      const ip = req.socket.remoteAddress;
      const port = req.socket.remotePort;
      res.end(`Your IP address is ${ip} and your source port is ${port}.`);
    }).listen(3000);
    ```
  + [statusCode](https://bun.com/reference/node/http2/Http2ServerResponse/statusCode): number

    When using implicit headers (not calling `response.writeHead()` explicitly), this property controls the status code that will be sent to the client when the headers get flushed.

    ```
    response.statusCode = 404;
    ```

    After response header was sent to the client, this property indicates the status code which was sent out.
  + [statusMessage](https://bun.com/reference/node/http2/Http2ServerResponse/statusMessage): ''

    Status message is not supported by HTTP/2 (RFC 7540 8.1.2.4). It returns an empty string.
  + readonly [stream](https://bun.com/reference/node/http2/Http2ServerResponse/stream): [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream)

    The `Http2Stream` object backing the response.
  + readonly [writable](https://bun.com/reference/node/http2/Http2ServerResponse/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http2/Http2ServerResponse/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http2/Http2ServerResponse/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http2/Http2ServerResponse/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http2/Http2ServerResponse/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http2/Http2ServerResponse/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http2/Http2ServerResponse/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http2/Http2ServerResponse/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http2/Http2ServerResponse/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/http2/Http2ServerResponse/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http2/Http2ServerResponse/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http2/Http2ServerResponse/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/http2/Http2ServerResponse/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http2/Http2ServerResponse/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http2/Http2ServerResponse/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http2/Http2ServerResponse/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_write](https://bun.com/reference/node/http2/Http2ServerResponse/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http2/Http2ServerResponse/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/Http2ServerResponse/[asyncDispose])(): Promise<void>;

    Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2ServerResponse/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2ServerResponse/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe
  + [addTrailers](https://bun.com/reference/node/http2/Http2ServerResponse/addTrailers)(

    trailers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): void;

    This method adds HTTP trailing headers (a header but at the end of the message) to the response.

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.
  + [appendHeader](https://bun.com/reference/node/http2/Http2ServerResponse/appendHeader)(

    name: string,

    value: string | string[]

    ): void;

    Append a single header value to the header object.

    If the value is an array, this is equivalent to calling this method multiple times.

    If there were no previous values for the header, this is equivalent to calling setHeader.

    Attempting to set a header field name or value that contains invalid characters will result in a [TypeError](https://nodejs.org/docs/latest-v24.x/api/errors.html#class-typeerror) being thrown.

    ```
    // Returns headers including "set-cookie: a" and "set-cookie: b"
    const server = http2.createServer((req, res) => {
      res.setHeader('set-cookie', 'a');
      res.appendHeader('set-cookie', 'b');
      res.writeHead(200);
      res.end('ok');
    });
    ```
  + [compose](https://bun.com/reference/node/http2/Http2ServerResponse/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http2/Http2ServerResponse/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [createPushResponse](https://bun.com/reference/node/http2/Http2ServerResponse/createPushResponse)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), res: [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)) => void

    ): void;

    Call `http2stream.pushStream()` with the given headers, and wrap the given `Http2Stream` on a newly created `Http2ServerResponse` as the callback parameter if successful. When `Http2ServerRequest` is closed, the callback is called with an error `ERR_HTTP2_INVALID_STREAM`.

    @param headers

    An object describing the headers

    @param callback

    Called once `http2stream.pushStream()` is finished, or either when the attempt to create the pushed `Http2Stream` has failed or has been rejected, or the state of `Http2ServerRequest` is closed prior to calling the `http2stream.pushStream()` method
  + [destroy](https://bun.com/reference/node/http2/Http2ServerResponse/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `writable._destroy()`.

    @param error

    Optional, an error to emit with `'error'` event.
  + [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'error',

    error: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2ServerResponse/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http2/Http2ServerResponse/end)(

    callback?: () => void

    ): this;

    This method signals to the server that all of the response headers and body have been sent; that server should consider this message complete. The method, `response.end()`, MUST be called on each response.

    If `data` is specified, it is equivalent to calling `response.write(data, encoding)` followed by `response.end(callback)`.

    If `callback` is specified, it will be called when the response stream is finished.

    [end](https://bun.com/reference/node/http2/Http2ServerResponse/end)(

    data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    callback?: () => void

    ): this;

    This method signals to the server that all of the response headers and body have been sent; that server should consider this message complete. The method, `response.end()`, MUST be called on each response.

    If `data` is specified, it is equivalent to calling `response.write(data, encoding)` followed by `response.end(callback)`.

    If `callback` is specified, it will be called when the response stream is finished.

    [end](https://bun.com/reference/node/http2/Http2ServerResponse/end)(

    data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding: BufferEncoding,

    callback?: () => void

    ): this;

    This method signals to the server that all of the response headers and body have been sent; that server should consider this message complete. The method, `response.end()`, MUST be called on each response.

    If `data` is specified, it is equivalent to calling `response.write(data, encoding)` followed by `response.end(callback)`.

    If `callback` is specified, it will be called when the response stream is finished.
  + [eventNames](https://bun.com/reference/node/http2/Http2ServerResponse/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getHeader](https://bun.com/reference/node/http2/Http2ServerResponse/getHeader)(

    name: string

    ): string;

    Reads out a header that has already been queued but not sent to the client. The name is case-insensitive.

    ```
    const contentType = response.getHeader('content-type');
    ```
  + [getHeaderNames](https://bun.com/reference/node/http2/Http2ServerResponse/getHeaderNames)(): string[];

    Returns an array containing the unique names of the current outgoing headers. All header names are lowercase.

    ```
    response.setHeader('Foo', 'bar');
    response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headerNames = response.getHeaderNames();
    // headerNames === ['foo', 'set-cookie']
    ```
  + [getHeaders](https://bun.com/reference/node/http2/Http2ServerResponse/getHeaders)(): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders);

    Returns a shallow copy of the current outgoing headers. Since a shallow copy is used, array values may be mutated without additional calls to various header-related http module methods. The keys of the returned object are the header names and the values are the respective header values. All header names are lowercase.

    The object returned by the `response.getHeaders()` method *does not* prototypically inherit from the JavaScript `Object`. This means that typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`, and others are not defined and *will not work*.

    ```
    response.setHeader('Foo', 'bar');
    response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headers = response.getHeaders();
    // headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
    ```
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2ServerResponse/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [hasHeader](https://bun.com/reference/node/http2/Http2ServerResponse/hasHeader)(

    name: string

    ): boolean;

    Returns `true` if the header identified by `name` is currently set in the outgoing headers. The header name matching is case-insensitive.

    ```
    const hasContentType = response.hasHeader('content-type');
    ```
  + [listenerCount](https://bun.com/reference/node/http2/Http2ServerResponse/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2ServerResponse/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/Http2ServerResponse/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pipe](https://bun.com/reference/node/http2/Http2ServerResponse/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2ServerResponse/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http2/Http2ServerResponse/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2ServerResponse/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeHeader](https://bun.com/reference/node/http2/Http2ServerResponse/removeHeader)(

    name: string

    ): void;

    Removes a header that has been queued for implicit sending.

    ```
    response.removeHeader('Content-Encoding');
    ```
  + [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2ServerResponse/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setDefaultEncoding](https://bun.com/reference/node/http2/Http2ServerResponse/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setHeader](https://bun.com/reference/node/http2/Http2ServerResponse/setHeader)(

    name: string,

    value: string | number | readonly string[]

    ): void;

    Sets a single header value for implicit headers. If this header already exists in the to-be-sent headers, its value will be replaced. Use an array of strings here to send multiple headers with the same name.

    ```
    response.setHeader('Content-Type', 'text/html; charset=utf-8');
    ```

    or

    ```
    response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.

    When headers have been set with `response.setHeader()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http2.createServer((req, res) => {
      res.setHeader('Content-Type', 'text/html; charset=utf-8');
      res.setHeader('X-Foo', 'bar');
      res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
      res.end('ok');
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2ServerResponse/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/Http2ServerResponse/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    Sets the `Http2Stream`'s timeout value to `msecs`. If a callback is provided, then it is added as a listener on the `'timeout'` event on the response object.

    If no `'timeout'` listener is added to the request, the response, or the server, then `Http2Stream` s are destroyed when they time out. If a handler is assigned to the request, the response, or the server's `'timeout'` events, timed out sockets must be handled explicitly.
  + [uncork](https://bun.com/reference/node/http2/Http2ServerResponse/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [write](https://bun.com/reference/node/http2/Http2ServerResponse/write)(

    chunk: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    callback?: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    If this method is called and `response.writeHead()` has not been called, it will switch to implicit header mode and flush the implicit headers.

    This sends a chunk of the response body. This method may be called multiple times to provide successive parts of the body.

    In the `node:http` module, the response body is omitted when the request is a HEAD request. Similarly, the `204` and `304` responses *must not* include a message body.

    `chunk` can be a string or a buffer. If `chunk` is a string, the second parameter specifies how to encode it into a byte stream. By default the `encoding` is `'utf8'`. `callback` will be called when this chunk of data is flushed.

    This is the raw HTTP body and has nothing to do with higher-level multi-part body encodings that may be used.

    The first time `response.write()` is called, it will send the buffered header information and the first chunk of the body to the client. The second time `response.write()` is called, Node.js assumes data will be streamed, and sends the new data separately. That is, the response is buffered up to the first chunk of the body.

    Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory.`'drain'` will be emitted when the buffer is free again.

    [write](https://bun.com/reference/node/http2/Http2ServerResponse/write)(

    chunk: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding: BufferEncoding,

    callback?: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    If this method is called and `response.writeHead()` has not been called, it will switch to implicit header mode and flush the implicit headers.

    This sends a chunk of the response body. This method may be called multiple times to provide successive parts of the body.

    In the `node:http` module, the response body is omitted when the request is a HEAD request. Similarly, the `204` and `304` responses *must not* include a message body.

    `chunk` can be a string or a buffer. If `chunk` is a string, the second parameter specifies how to encode it into a byte stream. By default the `encoding` is `'utf8'`. `callback` will be called when this chunk of data is flushed.

    This is the raw HTTP body and has nothing to do with higher-level multi-part body encodings that may be used.

    The first time `response.write()` is called, it will send the buffered header information and the first chunk of the body to the client. The second time `response.write()` is called, Node.js assumes data will be streamed, and sends the new data separately. That is, the response is buffered up to the first chunk of the body.

    Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory.`'drain'` will be emitted when the buffer is free again.
  + [writeContinue](https://bun.com/reference/node/http2/Http2ServerResponse/writeContinue)(): void;

    Sends a status `100 Continue` to the client, indicating that the request body should be sent. See the `'checkContinue'` event on `Http2Server` and `Http2SecureServer`.
  + [writeEarlyHints](https://bun.com/reference/node/http2/Http2ServerResponse/writeEarlyHints)(

    hints: Record<string, string | string[]>

    ): void;

    Sends a status `103 Early Hints` to the client with a Link header, indicating that the user agent can preload/preconnect the linked resources. The `hints` is an object containing the values of headers to be sent with early hints message.

    **Example**

    ```
    const earlyHintsLink = '</styles.css>; rel=preload; as=style';
    response.writeEarlyHints({
      'link': earlyHintsLink,
    });

    const earlyHintsLinks = [
      '</styles.css>; rel=preload; as=style',
      '</scripts.js>; rel=preload; as=script',
    ];
    response.writeEarlyHints({
      'link': earlyHintsLinks,
    });
    ```
  + [writeHead](https://bun.com/reference/node/http2/Http2ServerResponse/writeHead)(

    statusCode: number,

    headers?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): this;

    Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers.

    Returns a reference to the `Http2ServerResponse`, so that calls can be chained.

    For compatibility with `HTTP/1`, a human-readable `statusMessage` may be passed as the second argument. However, because the `statusMessage` has no meaning within HTTP/2, the argument will have no effect and a process warning will be emitted.

    ```
    const body = 'hello world';
    response.writeHead(200, {
      'Content-Length': Buffer.byteLength(body),
      'Content-Type': 'text/plain; charset=utf-8',
    });
    ```

    `Content-Length` is given in bytes not characters. The`Buffer.byteLength()` API may be used to determine the number of bytes in a given encoding. On outbound messages, Node.js does not check if Content-Length and the length of the body being transmitted are equal or not. However, when receiving messages, Node.js will automatically reject messages when the `Content-Length` does not match the actual payload size.

    This method may be called at most one time on a message before `response.end()` is called.

    If `response.write()` or `response.end()` are called before calling this, the implicit/mutable headers will be calculated and call this function.

    When headers have been set with `response.setHeader()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http2.createServer((req, res) => {
      res.setHeader('Content-Type', 'text/html; charset=utf-8');
      res.setHeader('X-Foo', 'bar');
      res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
      res.end('ok');
    });
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.

    [writeHead](https://bun.com/reference/node/http2/Http2ServerResponse/writeHead)(

    statusCode: number,

    statusMessage: string,

    headers?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): this;

    Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers.

    Returns a reference to the `Http2ServerResponse`, so that calls can be chained.

    For compatibility with `HTTP/1`, a human-readable `statusMessage` may be passed as the second argument. However, because the `statusMessage` has no meaning within HTTP/2, the argument will have no effect and a process warning will be emitted.

    ```
    const body = 'hello world';
    response.writeHead(200, {
      'Content-Length': Buffer.byteLength(body),
      'Content-Type': 'text/plain; charset=utf-8',
    });
    ```

    `Content-Length` is given in bytes not characters. The`Buffer.byteLength()` API may be used to determine the number of bytes in a given encoding. On outbound messages, Node.js does not check if Content-Length and the length of the body being transmitted are equal or not. However, when receiving messages, Node.js will automatically reject messages when the `Content-Length` does not match the actual payload size.

    This method may be called at most one time on a message before `response.end()` is called.

    If `response.write()` or `response.end()` are called before calling this, the implicit/mutable headers will be calculated and call this function.

    When headers have been set with `response.setHeader()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http2.createServer((req, res) => {
      res.setHeader('Content-Type', 'text/html; charset=utf-8');
      res.setHeader('X-Foo', 'bar');
      res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
      res.end('ok');
    });
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.
  + static [addAbortListener](https://bun.com/reference/node/http2/Http2ServerResponse/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [fromWeb](https://bun.com/reference/node/http2/Http2ServerResponse/fromWeb)(

    writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

    options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

    ): [Writable](https://bun.com/reference/node/stream/default/Writable);

    A utility method for creating a `Writable` from a web `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http2/Http2ServerResponse/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/http2/Http2ServerResponse/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/http2/Http2ServerResponse/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/http2/Http2ServerResponse/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/http2/Http2ServerResponse/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
  + static [toWeb](https://bun.com/reference/node/http2/Http2ServerResponse/toWeb)(

    streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

    ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

    A utility method for creating a web `WritableStream` from a `Writable`.
* const [sensitiveHeaders](https://bun.com/reference/node/http2/sensitiveHeaders): symbol

  This symbol can be set as a property on the HTTP/2 headers object with an array value in order to provide a list of headers considered sensitive.
* function [connect](https://bun.com/reference/node/http2/connect)(

  authority: string | [URL](https://bun.com/reference/node/url/URL),

  listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

  ): [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session);

  Returns a `ClientHttp2Session` instance.

  ```
  import http2 from 'node:http2';
  const client = http2.connect('https://localhost:1234');

  // Use the client

  client.close();
  ```

  @param authority

  The remote HTTP/2 server to connect to. This must be in the form of a minimal, valid URL with the `http://` or `https://` prefix, host name, and IP port (if a non-default port is used). Userinfo (user ID and password), path, querystring, and fragment details in the URL will be ignored.

  @param listener

  Will be registered as a one-time listener of the 'connect' event.

  function [connect](https://bun.com/reference/node/http2/connect)(

  authority: string | [URL](https://bun.com/reference/node/url/URL),

  options?: [ClientSessionOptions](https://bun.com/reference/node/http2/ClientSessionOptions) | [SecureClientSessionOptions](https://bun.com/reference/node/http2/SecureClientSessionOptions),

  listener?: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

  ): [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session);

  Returns a `ClientHttp2Session` instance.

  ```
  import http2 from 'node:http2';
  const client = http2.connect('https://localhost:1234');

  // Use the client

  client.close();
  ```

  @param authority

  The remote HTTP/2 server to connect to. This must be in the form of a minimal, valid URL with the `http://` or `https://` prefix, host name, and IP port (if a non-default port is used). Userinfo (user ID and password), path, querystring, and fragment details in the URL will be ignored.

  @param listener

  Will be registered as a one-time listener of the 'connect' event.
* function [createSecureServer](https://bun.com/reference/node/http2/createSecureServer)(

  onRequestHandler?: (request: [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), response: [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)) => void

  ): [Http2SecureServer](https://bun.com/reference/node/http2/Http2SecureServer);

  Returns a `tls.Server` instance that creates and manages `Http2Session` instances.

  ```
  import http2 from 'node:http2';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('server-key.pem'),
    cert: fs.readFileSync('server-cert.pem'),
  };

  // Create a secure HTTP/2 server
  const server = http2.createSecureServer(options);

  server.on('stream', (stream, headers) => {
    stream.respond({
      'content-type': 'text/html; charset=utf-8',
      ':status': 200,
    });
    stream.end('<h1>Hello World</h1>');
  });

  server.listen(8443);
  ```

  @param onRequestHandler

  See `Compatibility API`

  function [createSecureServer](https://bun.com/reference/node/http2/createSecureServer)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>(

  options: [SecureServerOptions](https://bun.com/reference/node/http2/SecureServerOptions)<Http1Request, Http1Response, Http2Request, Http2Response>,

  onRequestHandler?: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

  ): [Http2SecureServer](https://bun.com/reference/node/http2/Http2SecureServer)<Http1Request, Http1Response, Http2Request, Http2Response>;

  Returns a `tls.Server` instance that creates and manages `Http2Session` instances.

  ```
  import http2 from 'node:http2';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('server-key.pem'),
    cert: fs.readFileSync('server-cert.pem'),
  };

  // Create a secure HTTP/2 server
  const server = http2.createSecureServer(options);

  server.on('stream', (stream, headers) => {
    stream.respond({
      'content-type': 'text/html; charset=utf-8',
      ':status': 200,
    });
    stream.end('<h1>Hello World</h1>');
  });

  server.listen(8443);
  ```

  @param onRequestHandler

  See `Compatibility API`
* function [createServer](https://bun.com/reference/node/http2/createServer)(

  onRequestHandler?: (request: [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), response: [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)) => void

  ): [Http2Server](https://bun.com/reference/node/http2/Http2Server);

  Returns a `net.Server` instance that creates and manages `Http2Session` instances.

  Since there are no browsers known that support [unencrypted HTTP/2](https://http2.github.io/faq/#does-http2-require-encryption), the use of createSecureServer is necessary when communicating with browser clients.

  ```
  import http2 from 'node:http2';

  // Create an unencrypted HTTP/2 server.
  // Since there are no browsers known that support
  // unencrypted HTTP/2, the use of `http2.createSecureServer()`
  // is necessary when communicating with browser clients.
  const server = http2.createServer();

  server.on('stream', (stream, headers) => {
    stream.respond({
      'content-type': 'text/html; charset=utf-8',
      ':status': 200,
    });
    stream.end('<h1>Hello World</h1>');
  });

  server.listen(8000);
  ```

  @param onRequestHandler

  See `Compatibility API`

  function [createServer](https://bun.com/reference/node/http2/createServer)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>(

  options: [ServerOptions](https://bun.com/reference/node/http2/ServerOptions)<Http1Request, Http1Response, Http2Request, Http2Response>,

  onRequestHandler?: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

  ): [Http2Server](https://bun.com/reference/node/http2/Http2Server)<Http1Request, Http1Response, Http2Request, Http2Response>;

  Returns a `net.Server` instance that creates and manages `Http2Session` instances.

  Since there are no browsers known that support [unencrypted HTTP/2](https://http2.github.io/faq/#does-http2-require-encryption), the use of createSecureServer is necessary when communicating with browser clients.

  ```
  import http2 from 'node:http2';

  // Create an unencrypted HTTP/2 server.
  // Since there are no browsers known that support
  // unencrypted HTTP/2, the use of `http2.createSecureServer()`
  // is necessary when communicating with browser clients.
  const server = http2.createServer();

  server.on('stream', (stream, headers) => {
    stream.respond({
      'content-type': 'text/html; charset=utf-8',
      ':status': 200,
    });
    stream.end('<h1>Hello World</h1>');
  });

  server.listen(8000);
  ```

  @param onRequestHandler

  See `Compatibility API`
* function [getDefaultSettings](https://bun.com/reference/node/http2/getDefaultSettings)(): [Settings](https://bun.com/reference/node/http2/Settings);

  Returns an object containing the default settings for an `Http2Session` instance. This method returns a new object instance every time it is called so instances returned may be safely modified for use.
* function [getPackedSettings](https://bun.com/reference/node/http2/getPackedSettings)(

  settings: [Settings](https://bun.com/reference/node/http2/Settings)

  ): NonSharedBuffer;

  Returns a `Buffer` instance containing serialized representation of the given HTTP/2 settings as specified in the [HTTP/2](https://tools.ietf.org/html/rfc7540) specification. This is intended for use with the `HTTP2-Settings` header field.

  ```
  import http2 from 'node:http2';

  const packed = http2.getPackedSettings({ enablePush: false });

  console.log(packed.toString('base64'));
  // Prints: AAIAAAAA
  ```
* function [getUnpackedSettings](https://bun.com/reference/node/http2/getUnpackedSettings)(

  buf: [Uint8Array](https://bun.com/reference/globals/Uint8Array)

  ): [Settings](https://bun.com/reference/node/http2/Settings);

  Returns a `HTTP/2 Settings Object` containing the deserialized settings from the given `Buffer` as generated by `http2.getPackedSettings()`.

  @param buf

  The packed settings.
* function [performServerHandshake](https://bun.com/reference/node/http2/performServerHandshake)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>(

  socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

  options?: [ServerOptions](https://bun.com/reference/node/http2/ServerOptions)<Http1Request, Http1Response, Http2Request, Http2Response>

  ): [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>;

  Create an HTTP/2 server session from an existing socket.

  @param socket

  A Duplex Stream

  @param options

  Any `{@link createServer}` options can be provided.

## Type definitions

* ### interface [AlternativeServiceOptions](https://bun.com/reference/node/http2/AlternativeServiceOptions)

  + [origin](https://bun.com/reference/node/http2/AlternativeServiceOptions/origin): string | number | [URL](https://bun.com/reference/node/url/URL)
* ### interface [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + readonly [closed](https://bun.com/reference/node/http2/ClientHttp2Session/closed): boolean

    Will be `true` if this `Http2Session` instance has been closed, otherwise `false`.
  + readonly [connecting](https://bun.com/reference/node/http2/ClientHttp2Session/connecting): boolean

    Will be `true` if this `Http2Session` instance is still connecting, will be set to `false` before emitting `connect` event and/or calling the `http2.connect` callback.
  + readonly [destroyed](https://bun.com/reference/node/http2/ClientHttp2Session/destroyed): boolean

    Will be `true` if this `Http2Session` instance has been destroyed and must no longer be used, otherwise `false`.
  + readonly [encrypted](https://bun.com/reference/node/http2/ClientHttp2Session/encrypted)?: boolean

    Value is `undefined` if the `Http2Session` session socket has not yet been connected, `true` if the `Http2Session` is connected with a `TLSSocket`, and `false` if the `Http2Session` is connected to any other kind of socket or stream.
  + readonly [localSettings](https://bun.com/reference/node/http2/ClientHttp2Session/localSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current local settings of this `Http2Session`. The local settings are local to *this*`Http2Session` instance.
  + readonly [originSet](https://bun.com/reference/node/http2/ClientHttp2Session/originSet)?: string[]

    If the `Http2Session` is connected to a `TLSSocket`, the `originSet` property will return an `Array` of origins for which the `Http2Session` may be considered authoritative.

    The `originSet` property is only available when using a secure TLS connection.
  + readonly [pendingSettingsAck](https://bun.com/reference/node/http2/ClientHttp2Session/pendingSettingsAck): boolean

    Indicates whether the `Http2Session` is currently waiting for acknowledgment of a sent `SETTINGS` frame. Will be `true` after calling the `http2session.settings()` method. Will be `false` once all sent `SETTINGS` frames have been acknowledged.
  + readonly [remoteSettings](https://bun.com/reference/node/http2/ClientHttp2Session/remoteSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current remote settings of this`Http2Session`. The remote settings are set by the *connected* HTTP/2 peer.
  + readonly [socket](https://bun.com/reference/node/http2/ClientHttp2Session/socket): [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    Returns a `Proxy` object that acts as a `net.Socket` (or `tls.TLSSocket`) but limits available methods to ones safe to use with HTTP/2.

    `destroy`, `emit`, `end`, `pause`, `read`, `resume`, and `write` will throw an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See `Http2Session and Sockets` for more information.

    `setTimeout` method will be called on this `Http2Session`.

    All other interactions will be routed directly to the socket.
  + readonly [state](https://bun.com/reference/node/http2/ClientHttp2Session/state): [SessionState](https://bun.com/reference/node/http2/SessionState)

    Provides miscellaneous information about the current state of the`Http2Session`.

    An object describing the current status of this `Http2Session`.
  + readonly [type](https://bun.com/reference/node/http2/ClientHttp2Session/type): number

    The `http2session.type` will be equal to `http2.constants.NGHTTP2_SESSION_SERVER` if this `Http2Session` instance is a server, and `http2.constants.NGHTTP2_SESSION_CLIENT` if the instance is a client.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/ClientHttp2Session/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/ClientHttp2Session/addListener)(

    event: 'altsvc',

    listener: (alt: string, origin: string, stream: number) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Session/addListener)(

    event: 'origin',

    listener: (origins: string[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Session/addListener)(

    event: 'connect',

    listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Session/addListener)(

    event: 'stream',

    listener: (stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Session/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [close](https://bun.com/reference/node/http2/ClientHttp2Session/close)(

    callback?: () => void

    ): void;

    Gracefully closes the `Http2Session`, allowing any existing streams to complete on their own and preventing new `Http2Stream` instances from being created. Once closed, `http2session.destroy()`*might* be called if there are no open `Http2Stream` instances.

    If specified, the `callback` function is registered as a handler for the`'close'` event.
  + [destroy](https://bun.com/reference/node/http2/ClientHttp2Session/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error),

    code?: number

    ): void;

    Immediately terminates the `Http2Session` and the associated `net.Socket` or `tls.TLSSocket`.

    Once destroyed, the `Http2Session` will emit the `'close'` event. If `error` is not undefined, an `'error'` event will be emitted immediately before the `'close'` event.

    If there are any remaining open `Http2Streams` associated with the `Http2Session`, those will also be destroyed.

    @param error

    An `Error` object if the `Http2Session` is being destroyed due to an error.

    @param code

    The HTTP/2 error code to send in the final `GOAWAY` frame. If unspecified, and `error` is not undefined, the default is `INTERNAL_ERROR`, otherwise defaults to `NO_ERROR`.
  + [emit](https://bun.com/reference/node/http2/ClientHttp2Session/emit)(

    event: 'altsvc',

    alt: string,

    origin: string,

    stream: number

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ClientHttp2Session/emit)(

    event: 'origin',

    origins: readonly string[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ClientHttp2Session/emit)(

    event: 'connect',

    session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session),

    socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ClientHttp2Session/emit)(

    event: 'stream',

    stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream),

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader),

    flags: number,

    rawHeaders: string[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ClientHttp2Session/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [eventNames](https://bun.com/reference/node/http2/ClientHttp2Session/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/http2/ClientHttp2Session/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [goaway](https://bun.com/reference/node/http2/ClientHttp2Session/goaway)(

    code?: number,

    lastStreamID?: number,

    opaqueData?: ArrayBufferView<ArrayBufferLike>

    ): void;

    Transmits a `GOAWAY` frame to the connected peer *without* shutting down the`Http2Session`.

    @param code

    An HTTP/2 error code

    @param lastStreamID

    The numeric ID of the last processed `Http2Stream`

    @param opaqueData

    A `TypedArray` or `DataView` instance containing additional data to be carried within the `GOAWAY` frame.
  + [listenerCount](https://bun.com/reference/node/http2/ClientHttp2Session/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/ClientHttp2Session/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/ClientHttp2Session/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/ClientHttp2Session/on)(

    event: 'altsvc',

    listener: (alt: string, origin: string, stream: number) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ClientHttp2Session/on)(

    event: 'origin',

    listener: (origins: string[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ClientHttp2Session/on)(

    event: 'connect',

    listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ClientHttp2Session/on)(

    event: 'stream',

    listener: (stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ClientHttp2Session/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/http2/ClientHttp2Session/once)(

    event: 'altsvc',

    listener: (alt: string, origin: string, stream: number) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ClientHttp2Session/once)(

    event: 'origin',

    listener: (origins: string[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ClientHttp2Session/once)(

    event: 'connect',

    listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ClientHttp2Session/once)(

    event: 'stream',

    listener: (stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ClientHttp2Session/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [ping](https://bun.com/reference/node/http2/ClientHttp2Session/ping)(

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;

    Sends a `PING` frame to the connected HTTP/2 peer. A `callback` function must be provided. The method will return `true` if the `PING` was sent, `false` otherwise.

    The maximum number of outstanding (unacknowledged) pings is determined by the `maxOutstandingPings` configuration option. The default maximum is 10.

    If provided, the `payload` must be a `Buffer`, `TypedArray`, or `DataView` containing 8 bytes of data that will be transmitted with the `PING` and returned with the ping acknowledgment.

    The callback will be invoked with three arguments: an error argument that will be `null` if the `PING` was successfully acknowledged, a `duration` argument that reports the number of milliseconds elapsed since the ping was sent and the acknowledgment was received, and a `Buffer` containing the 8-byte `PING` payload.

    ```
    session.ping(Buffer.from('abcdefgh'), (err, duration, payload) => {
      if (!err) {
        console.log(`Ping acknowledged in ${duration} milliseconds`);
        console.log(`With payload '${payload.toString()}'`);
      }
    });
    ```

    If the `payload` argument is not specified, the default payload will be the 64-bit timestamp (little endian) marking the start of the `PING` duration.

    [ping](https://bun.com/reference/node/http2/ClientHttp2Session/ping)(

    payload: ArrayBufferView,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;
  + [prependListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependListener)(

    event: 'altsvc',

    listener: (alt: string, origin: string, stream: number) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependListener)(

    event: 'origin',

    listener: (origins: string[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependListener)(

    event: 'connect',

    listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependListener)(

    event: 'stream',

    listener: (stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependOnceListener)(

    event: 'altsvc',

    listener: (alt: string, origin: string, stream: number) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependOnceListener)(

    event: 'origin',

    listener: (origins: string[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependOnceListener)(

    event: 'connect',

    listener: (session: [ClientHttp2Session](https://bun.com/reference/node/http2/ClientHttp2Session), socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependOnceListener)(

    event: 'stream',

    listener: (stream: [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Session/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/http2/ClientHttp2Session/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/http2/ClientHttp2Session/ref)(): void;

    Calls `ref()` on this `Http2Session` instance's underlying `net.Socket`.
  + [removeAllListeners](https://bun.com/reference/node/http2/ClientHttp2Session/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/ClientHttp2Session/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [request](https://bun.com/reference/node/http2/ClientHttp2Session/request)(

    headers?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    options?: [ClientSessionRequestOptions](https://bun.com/reference/node/http2/ClientSessionRequestOptions)

    ): [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream);

    For HTTP/2 Client `Http2Session` instances only, the `http2session.request()` creates and returns an `Http2Stream` instance that can be used to send an HTTP/2 request to the connected server.

    When a `ClientHttp2Session` is first created, the socket may not yet be connected. if `clienthttp2session.request()` is called during this time, the actual request will be deferred until the socket is ready to go. If the `session` is closed before the actual request be executed, an `ERR_HTTP2_GOAWAY_SESSION` is thrown.

    This method is only available if `http2session.type` is equal to `http2.constants.NGHTTP2_SESSION_CLIENT`.

    ```
    import http2 from 'node:http2';
    const clientSession = http2.connect('https://localhost:1234');
    const {
      HTTP2_HEADER_PATH,
      HTTP2_HEADER_STATUS,
    } = http2.constants;

    const req = clientSession.request({ [HTTP2_HEADER_PATH]: '/' });
    req.on('response', (headers) => {
      console.log(headers[HTTP2_HEADER_STATUS]);
      req.on('data', (chunk) => { // ..  });
      req.on('end', () => { // ..  });
    });
    ```

    When the `options.waitForTrailers` option is set, the `'wantTrailers'` event is emitted immediately after queuing the last chunk of payload data to be sent. The `http2stream.sendTrailers()` method can then be called to send trailing headers to the peer.

    When `options.waitForTrailers` is set, the `Http2Stream` will not automatically close when the final `DATA` frame is transmitted. User code must call either`http2stream.sendTrailers()` or `http2stream.close()` to close the`Http2Stream`.

    When `options.signal` is set with an `AbortSignal` and then `abort` on the corresponding `AbortController` is called, the request will emit an `'error'`event with an `AbortError` error.

    The `:method` and `:path` pseudo-headers are not specified within `headers`, they respectively default to:

    - `:method` = `'GET'`
    - `:path` = `/`
  + [setLocalWindowSize](https://bun.com/reference/node/http2/ClientHttp2Session/setLocalWindowSize)(

    windowSize: number

    ): void;

    Sets the local endpoint's window size. The `windowSize` is the total window size to set, not the delta.

    ```
    import http2 from 'node:http2';

    const server = http2.createServer();
    const expectedWindowSize = 2 ** 20;
    server.on('connect', (session) => {

      // Set local window size to be 2 ** 20
      session.setLocalWindowSize(expectedWindowSize);
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http2/ClientHttp2Session/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/ClientHttp2Session/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    Used to set a callback function that is called when there is no activity on the `Http2Session` after `msecs` milliseconds. The given `callback` is registered as a listener on the `'timeout'` event.
  + [settings](https://bun.com/reference/node/http2/ClientHttp2Session/settings)(

    settings: [Settings](https://bun.com/reference/node/http2/Settings),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), settings: [Settings](https://bun.com/reference/node/http2/Settings), duration: number) => void

    ): void;

    Updates the current local settings for this `Http2Session` and sends a new `SETTINGS` frame to the connected HTTP/2 peer.

    Once called, the `http2session.pendingSettingsAck` property will be `true` while the session is waiting for the remote peer to acknowledge the new settings.

    The new settings will not become effective until the `SETTINGS` acknowledgment is received and the `'localSettings'` event is emitted. It is possible to send multiple `SETTINGS` frames while acknowledgment is still pending.

    @param callback

    Callback that is called once the session is connected or right away if the session is already connected.
  + [unref](https://bun.com/reference/node/http2/ClientHttp2Session/unref)(): void;

    Calls `unref()` on this `Http2Session`instance's underlying `net.Socket`.
* ### interface [ClientHttp2Stream](https://bun.com/reference/node/http2/ClientHttp2Stream)

  Duplex streams are streams that implement both the `Readable` and `Writable` interfaces.

  Examples of `Duplex` streams include:

  + `TCP sockets`
  + `zlib streams`
  + `crypto streams`

  + readonly [aborted](https://bun.com/reference/node/http2/ClientHttp2Stream/aborted): boolean

    Set to `true` if the `Http2Stream` instance was aborted abnormally. When set, the `'aborted'` event will have been emitted.
  + [allowHalfOpen](https://bun.com/reference/node/http2/ClientHttp2Stream/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bufferSize](https://bun.com/reference/node/http2/ClientHttp2Stream/bufferSize): number

    This property shows the number of characters currently buffered to be written. See `net.Socket.bufferSize` for details.
  + readonly [closed](https://bun.com/reference/node/http2/ClientHttp2Stream/closed): boolean

    Set to `true` if the `Http2Stream` instance has been closed.
  + readonly [destroyed](https://bun.com/reference/node/http2/ClientHttp2Stream/destroyed): boolean

    Set to `true` if the `Http2Stream` instance has been destroyed and is no longer usable.
  + readonly [endAfterHeaders](https://bun.com/reference/node/http2/ClientHttp2Stream/endAfterHeaders): boolean

    Set to `true` if the `END_STREAM` flag was set in the request or response HEADERS frame received, indicating that no additional data should be received and the readable side of the `Http2Stream` will be closed.
  + readonly [errored](https://bun.com/reference/node/http2/ClientHttp2Stream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [id](https://bun.com/reference/node/http2/ClientHttp2Stream/id)?: number

    The numeric stream identifier of this `Http2Stream` instance. Set to `undefined` if the stream identifier has not yet been assigned.
  + readonly [pending](https://bun.com/reference/node/http2/ClientHttp2Stream/pending): boolean

    Set to `true` if the `Http2Stream` instance has not yet been assigned a numeric stream identifier.
  + [readable](https://bun.com/reference/node/http2/ClientHttp2Stream/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/http2/ClientHttp2Stream/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/http2/ClientHttp2Stream/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/http2/ClientHttp2Stream/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/http2/ClientHttp2Stream/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/http2/ClientHttp2Stream/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/http2/ClientHttp2Stream/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/http2/ClientHttp2Stream/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/http2/ClientHttp2Stream/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [rstCode](https://bun.com/reference/node/http2/ClientHttp2Stream/rstCode): number

    Set to the `RST_STREAM` `error code` reported when the `Http2Stream` is destroyed after either receiving an `RST_STREAM` frame from the connected peer, calling `http2stream.close()`, or `http2stream.destroy()`. Will be `undefined` if the `Http2Stream` has not been closed.
  + readonly [sentHeaders](https://bun.com/reference/node/http2/ClientHttp2Stream/sentHeaders): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound headers sent for this `Http2Stream`.
  + readonly [sentInfoHeaders](https://bun.com/reference/node/http2/ClientHttp2Stream/sentInfoHeaders)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)[]

    An array of objects containing the outbound informational (additional) headers sent for this `Http2Stream`.
  + readonly [sentTrailers](https://bun.com/reference/node/http2/ClientHttp2Stream/sentTrailers)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound trailers sent for this `HttpStream`.
  + readonly [session](https://bun.com/reference/node/http2/ClientHttp2Stream/session): undefined | [Http2Session](https://bun.com/reference/node/http2/Http2Session)

    A reference to the `Http2Session` instance that owns this `Http2Stream`. The value will be `undefined` after the `Http2Stream` instance is destroyed.
  + readonly [state](https://bun.com/reference/node/http2/ClientHttp2Stream/state): [StreamState](https://bun.com/reference/node/http2/StreamState)

    Provides miscellaneous information about the current state of the `Http2Stream`.

    A current state of this `Http2Stream`.
  + readonly [writable](https://bun.com/reference/node/http2/ClientHttp2Stream/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http2/ClientHttp2Stream/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http2/ClientHttp2Stream/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http2/ClientHttp2Stream/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http2/ClientHttp2Stream/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http2/ClientHttp2Stream/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http2/ClientHttp2Stream/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http2/ClientHttp2Stream/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http2/ClientHttp2Stream/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/http2/ClientHttp2Stream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http2/ClientHttp2Stream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http2/ClientHttp2Stream/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/http2/ClientHttp2Stream/_read)(

    size: number

    ): void;
  + [\_write](https://bun.com/reference/node/http2/ClientHttp2Stream/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http2/ClientHttp2Stream/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/ClientHttp2Stream/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/http2/ClientHttp2Stream/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/ClientHttp2Stream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/ClientHttp2Stream/addListener)(

    event: 'continue',

    listener: () => {}

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Stream/addListener)(

    event: 'headers',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Stream/addListener)(

    event: 'push',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Stream/addListener)(

    event: 'response',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ClientHttp2Stream/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/http2/ClientHttp2Stream/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/http2/ClientHttp2Stream/close)(

    code?: number,

    callback?: () => void

    ): void;

    Closes the `Http2Stream` instance by sending an `RST_STREAM` frame to the connected HTTP/2 peer.

    @param code

    Unsigned 32-bit integer identifying the error code.

    @param callback

    An optional function registered to listen for the `'close'` event.
  + [compose](https://bun.com/reference/node/http2/ClientHttp2Stream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http2/ClientHttp2Stream/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http2/ClientHttp2Stream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/http2/ClientHttp2Stream/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/http2/ClientHttp2Stream/emit)(

    event: 'continue'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ClientHttp2Stream/emit)(

    event: 'headers',

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader),

    flags: number,

    rawHeaders: string[]

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ClientHttp2Stream/emit)(

    event: 'push',

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ClientHttp2Stream/emit)(

    event: 'response',

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader),

    flags: number,

    rawHeaders: string[]

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ClientHttp2Stream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http2/ClientHttp2Stream/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http2/ClientHttp2Stream/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http2/ClientHttp2Stream/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http2/ClientHttp2Stream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/http2/ClientHttp2Stream/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/http2/ClientHttp2Stream/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/http2/ClientHttp2Stream/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/http2/ClientHttp2Stream/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/http2/ClientHttp2Stream/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/http2/ClientHttp2Stream/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/http2/ClientHttp2Stream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/http2/ClientHttp2Stream/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/http2/ClientHttp2Stream/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/http2/ClientHttp2Stream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/ClientHttp2Stream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/http2/ClientHttp2Stream/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/http2/ClientHttp2Stream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/ClientHttp2Stream/on)(

    event: 'continue',

    listener: () => {}

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ClientHttp2Stream/on)(

    event: 'headers',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ClientHttp2Stream/on)(

    event: 'push',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ClientHttp2Stream/on)(

    event: 'response',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ClientHttp2Stream/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/ClientHttp2Stream/once)(

    event: 'continue',

    listener: () => {}

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ClientHttp2Stream/once)(

    event: 'headers',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ClientHttp2Stream/once)(

    event: 'push',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ClientHttp2Stream/once)(

    event: 'response',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ClientHttp2Stream/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/http2/ClientHttp2Stream/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/http2/ClientHttp2Stream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependListener)(

    event: 'continue',

    listener: () => {}

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependListener)(

    event: 'headers',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependListener)(

    event: 'push',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependListener)(

    event: 'response',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependOnceListener)(

    event: 'continue',

    listener: () => {}

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependOnceListener)(

    event: 'headers',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependOnceListener)(

    event: 'push',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependOnceListener)(

    event: 'response',

    listener: (headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders) & [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ClientHttp2Stream/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/http2/ClientHttp2Stream/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/http2/ClientHttp2Stream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/http2/ClientHttp2Stream/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/http2/ClientHttp2Stream/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/http2/ClientHttp2Stream/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/http2/ClientHttp2Stream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ClientHttp2Stream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/http2/ClientHttp2Stream/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [sendTrailers](https://bun.com/reference/node/http2/ClientHttp2Stream/sendTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): void;

    Sends a trailing `HEADERS` frame to the connected HTTP/2 peer. This method will cause the `Http2Stream` to be immediately closed and must only be called after the `'wantTrailers'` event has been emitted. When sending a request or sending a response, the `options.waitForTrailers` option must be set in order to keep the `Http2Stream` open after the final `DATA` frame so that trailers can be sent.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond(undefined, { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ xyz: 'abc' });
      });
      stream.end('Hello World');
    });
    ```

    The HTTP/1 specification forbids trailers from containing HTTP/2 pseudo-header fields (e.g. `':method'`, `':path'`, etc).
  + [setDefaultEncoding](https://bun.com/reference/node/http2/ClientHttp2Stream/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/http2/ClientHttp2Stream/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/http2/ClientHttp2Stream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/ClientHttp2Stream/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    ```
    import http2 from 'node:http2';
    const client = http2.connect('http://example.org:8000');
    const { NGHTTP2_CANCEL } = http2.constants;
    const req = client.request({ ':path': '/' });

    // Cancel the stream if there's no activity after 5 seconds
    req.setTimeout(5000, () => req.close(NGHTTP2_CANCEL));
    ```
  + [some](https://bun.com/reference/node/http2/ClientHttp2Stream/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/http2/ClientHttp2Stream/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/http2/ClientHttp2Stream/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/http2/ClientHttp2Stream/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/http2/ClientHttp2Stream/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/http2/ClientHttp2Stream/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/http2/ClientHttp2Stream/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/http2/ClientHttp2Stream/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http2/ClientHttp2Stream/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [ClientSessionOptions](https://bun.com/reference/node/http2/ClientSessionOptions)

  + [createConnection](https://bun.com/reference/node/http2/ClientSessionOptions/createConnection)?: (authority: [URL](https://bun.com/reference/node/url/URL), option: [SessionOptions](https://bun.com/reference/node/http2/SessionOptions)) => [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    An optional callback that receives the `URL` instance passed to `connect` and the `options` object, and returns any `Duplex` stream that is to be used as the connection for this session.
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/ClientSessionOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/ClientSessionOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/ClientSessionOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxReservedRemoteStreams](https://bun.com/reference/node/http2/ClientSessionOptions/maxReservedRemoteStreams)?: number

    Sets the maximum number of reserved push streams the client will accept at any given time. Once the current number of currently reserved push streams exceeds reaches this limit, new push streams sent by the server will be automatically rejected. The minimum allowed value is 0. The maximum allowed value is 2<sup>32</sup>-1. A negative value sets this option to the maximum allowed value.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/ClientSessionOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/ClientSessionOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/ClientSessionOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [paddingStrategy](https://bun.com/reference/node/http2/ClientSessionOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/ClientSessionOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/ClientSessionOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [settings](https://bun.com/reference/node/http2/ClientSessionOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/ClientSessionOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
* ### interface [ClientSessionRequestOptions](https://bun.com/reference/node/http2/ClientSessionRequestOptions)

  + [endStream](https://bun.com/reference/node/http2/ClientSessionRequestOptions/endStream)?: boolean
  + [exclusive](https://bun.com/reference/node/http2/ClientSessionRequestOptions/exclusive)?: boolean
  + [parent](https://bun.com/reference/node/http2/ClientSessionRequestOptions/parent)?: number
  + [signal](https://bun.com/reference/node/http2/ClientSessionRequestOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [waitForTrailers](https://bun.com/reference/node/http2/ClientSessionRequestOptions/waitForTrailers)?: boolean
* ### interface [Http2SecureServer](https://bun.com/reference/node/http2/Http2SecureServer)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  Accepts encrypted connections using TLS or SSL.

  + [connections](https://bun.com/reference/node/http2/Http2SecureServer/connections): number
  + readonly [listening](https://bun.com/reference/node/http2/Http2SecureServer/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/http2/Http2SecureServer/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/Http2SecureServer/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2SecureServer/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addContext](https://bun.com/reference/node/http2/Http2SecureServer/addContext)(

    hostname: string,

    context: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions) | [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    ): void;

    The `server.addContext()` method adds a secure context that will be used if the client request's SNI name matches the supplied `hostname` (or wildcard).

    When there are multiple matching contexts, the most recently added one is used.

    @param hostname

    A SNI host name or wildcard (e.g. `'*'`)

    @param context

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc), or a TLS context object created with createSecureContext itself.
  + [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: 'unknownProtocol',

    listener: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/http2/Http2SecureServer/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog
  + [address](https://bun.com/reference/node/http2/Http2SecureServer/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns the bound `address`, the address `family` name, and `port` of the server as reported by the operating system if listening on an IP socket (useful to find which port was assigned when getting an OS-assigned address):`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`.

    For a server listening on a pipe or Unix domain socket, the name is returned as a string.

    ```
    const server = net.createServer((socket) => {
      socket.end('goodbye\n');
    }).on('error', (err) => {
      // Handle errors here.
      throw err;
    });

    // Grab an arbitrary unused port.
    server.listen(() => {
      console.log('opened server on', server.address());
    });
    ```

    `server.address()` returns `null` before the `'listening'` event has been emitted or after calling `server.close()`.
  + [close](https://bun.com/reference/node/http2/Http2SecureServer/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'checkContinue',

    request: InstanceType<Http2Request>,

    response: InstanceType<Http2Response>

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'request',

    request: InstanceType<Http2Request>,

    response: InstanceType<Http2Response>

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'session',

    session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'sessionError',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'stream',

    stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream),

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'timeout'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: 'unknownProtocol',

    socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2SecureServer/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/http2/Http2SecureServer/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getConnections](https://bun.com/reference/node/http2/Http2SecureServer/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2SecureServer/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getTicketKeys](https://bun.com/reference/node/http2/Http2SecureServer/getTicketKeys)(): NonSharedBuffer;

    Returns the session ticket keys.

    See `Session Resumption` for more information.

    @returns

    A 48-byte buffer containing the session ticket keys.
  + [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    port?: number,

    hostname?: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    port?: number,

    hostname?: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    port?: number,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    port?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    path: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    path: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    options: [ListenOptions](https://bun.com/reference/node/net/ListenOptions),

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    handle: any,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2SecureServer/listen)(

    handle: any,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```
  + [listenerCount](https://bun.com/reference/node/http2/Http2SecureServer/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2SecureServer/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/Http2SecureServer/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'timeout',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: 'unknownProtocol',

    listener: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2SecureServer/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'timeout',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: 'unknownProtocol',

    listener: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2SecureServer/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: 'unknownProtocol',

    listener: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2SecureServer/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: 'unknownProtocol',

    listener: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2SecureServer/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http2/Http2SecureServer/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/http2/Http2SecureServer/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2SecureServer/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/Http2SecureServer/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2SecureServer/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setSecureContext](https://bun.com/reference/node/http2/Http2SecureServer/setSecureContext)(

    options: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions)

    ): void;

    The `server.setSecureContext()` method replaces the secure context of an existing server. Existing connections to the server are not interrupted.

    @param options

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc).
  + [setTicketKeys](https://bun.com/reference/node/http2/Http2SecureServer/setTicketKeys)(

    keys: [Buffer](https://bun.com/reference/node/buffer/Buffer)

    ): void;

    Sets the session ticket keys.

    Changes to the ticket keys are effective only for future server connections. Existing or currently pending server connections will use the previous keys.

    See `Session Resumption` for more information.

    @param keys

    A 48-byte buffer containing the session ticket keys.
  + [setTimeout](https://bun.com/reference/node/http2/Http2SecureServer/setTimeout)(

    msec?: number,

    callback?: () => void

    ): this;
  + [unref](https://bun.com/reference/node/http2/Http2SecureServer/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + [updateSettings](https://bun.com/reference/node/http2/Http2SecureServer/updateSettings)(

    settings: [Settings](https://bun.com/reference/node/http2/Settings)

    ): void;

    Throws ERR\_HTTP2\_INVALID\_SETTING\_VALUE for invalid settings values. Throws ERR\_INVALID\_ARG\_TYPE for invalid settings argument.
* ### interface [Http2Server](https://bun.com/reference/node/http2/Http2Server)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  This class is used to create a TCP or `IPC` server.

  + [connections](https://bun.com/reference/node/http2/Http2Server/connections): number
  + readonly [listening](https://bun.com/reference/node/http2/Http2Server/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/http2/Http2Server/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/Http2Server/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2Server/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http2/Http2Server/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop
  + [address](https://bun.com/reference/node/http2/Http2Server/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns the bound `address`, the address `family` name, and `port` of the server as reported by the operating system if listening on an IP socket (useful to find which port was assigned when getting an OS-assigned address):`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`.

    For a server listening on a pipe or Unix domain socket, the name is returned as a string.

    ```
    const server = net.createServer((socket) => {
      socket.end('goodbye\n');
    }).on('error', (err) => {
      // Handle errors here.
      throw err;
    });

    // Grab an arbitrary unused port.
    server.listen(() => {
      console.log('opened server on', server.address());
    });
    ```

    `server.address()` returns `null` before the `'listening'` event has been emitted or after calling `server.close()`.
  + [close](https://bun.com/reference/node/http2/Http2Server/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'checkContinue',

    request: InstanceType<Http2Request>,

    response: InstanceType<Http2Response>

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'request',

    request: InstanceType<Http2Request>,

    response: InstanceType<Http2Response>

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'session',

    session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'sessionError',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'stream',

    stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream),

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number,

    rawHeaders: string[]

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: 'timeout'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Server/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/http2/Http2Server/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getConnections](https://bun.com/reference/node/http2/Http2Server/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2Server/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    port?: number,

    hostname?: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    port?: number,

    hostname?: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    port?: number,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    port?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    path: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    path: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    options: [ListenOptions](https://bun.com/reference/node/net/ListenOptions),

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    handle: any,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/http2/Http2Server/listen)(

    handle: any,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```
  + [listenerCount](https://bun.com/reference/node/http2/Http2Server/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2Server/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/Http2Server/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: 'timeout',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Server/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: 'timeout',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Server/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Server/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'checkContinue',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'request',

    listener: (request: InstanceType<Http2Request>, response: InstanceType<Http2Response>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'session',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'sessionError',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Server/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http2/Http2Server/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/http2/Http2Server/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2Server/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/Http2Server/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2Server/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/Http2Server/setTimeout)(

    msec?: number,

    callback?: () => void

    ): this;
  + [unref](https://bun.com/reference/node/http2/Http2Server/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + [updateSettings](https://bun.com/reference/node/http2/Http2Server/updateSettings)(

    settings: [Settings](https://bun.com/reference/node/http2/Settings)

    ): void;

    Throws ERR\_HTTP2\_INVALID\_SETTING\_VALUE for invalid settings values. Throws ERR\_INVALID\_ARG\_TYPE for invalid settings argument.
* ### interface [Http2Session](https://bun.com/reference/node/http2/Http2Session)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + readonly [closed](https://bun.com/reference/node/http2/Http2Session/closed): boolean

    Will be `true` if this `Http2Session` instance has been closed, otherwise `false`.
  + readonly [connecting](https://bun.com/reference/node/http2/Http2Session/connecting): boolean

    Will be `true` if this `Http2Session` instance is still connecting, will be set to `false` before emitting `connect` event and/or calling the `http2.connect` callback.
  + readonly [destroyed](https://bun.com/reference/node/http2/Http2Session/destroyed): boolean

    Will be `true` if this `Http2Session` instance has been destroyed and must no longer be used, otherwise `false`.
  + readonly [encrypted](https://bun.com/reference/node/http2/Http2Session/encrypted)?: boolean

    Value is `undefined` if the `Http2Session` session socket has not yet been connected, `true` if the `Http2Session` is connected with a `TLSSocket`, and `false` if the `Http2Session` is connected to any other kind of socket or stream.
  + readonly [localSettings](https://bun.com/reference/node/http2/Http2Session/localSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current local settings of this `Http2Session`. The local settings are local to *this*`Http2Session` instance.
  + readonly [originSet](https://bun.com/reference/node/http2/Http2Session/originSet)?: string[]

    If the `Http2Session` is connected to a `TLSSocket`, the `originSet` property will return an `Array` of origins for which the `Http2Session` may be considered authoritative.

    The `originSet` property is only available when using a secure TLS connection.
  + readonly [pendingSettingsAck](https://bun.com/reference/node/http2/Http2Session/pendingSettingsAck): boolean

    Indicates whether the `Http2Session` is currently waiting for acknowledgment of a sent `SETTINGS` frame. Will be `true` after calling the `http2session.settings()` method. Will be `false` once all sent `SETTINGS` frames have been acknowledged.
  + readonly [remoteSettings](https://bun.com/reference/node/http2/Http2Session/remoteSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current remote settings of this`Http2Session`. The remote settings are set by the *connected* HTTP/2 peer.
  + readonly [socket](https://bun.com/reference/node/http2/Http2Session/socket): [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    Returns a `Proxy` object that acts as a `net.Socket` (or `tls.TLSSocket`) but limits available methods to ones safe to use with HTTP/2.

    `destroy`, `emit`, `end`, `pause`, `read`, `resume`, and `write` will throw an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See `Http2Session and Sockets` for more information.

    `setTimeout` method will be called on this `Http2Session`.

    All other interactions will be routed directly to the socket.
  + readonly [state](https://bun.com/reference/node/http2/Http2Session/state): [SessionState](https://bun.com/reference/node/http2/SessionState)

    Provides miscellaneous information about the current state of the`Http2Session`.

    An object describing the current status of this `Http2Session`.
  + readonly [type](https://bun.com/reference/node/http2/Http2Session/type): number

    The `http2session.type` will be equal to `http2.constants.NGHTTP2_SESSION_SERVER` if this `Http2Session` instance is a server, and `http2.constants.NGHTTP2_SESSION_CLIENT` if the instance is a client.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2Session/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number, streamID: number) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'goaway',

    listener: (errorCode: number, lastStreamID: number, opaqueData?: NonSharedBuffer) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'localSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'ping',

    listener: () => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'remoteSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/Http2Session/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [close](https://bun.com/reference/node/http2/Http2Session/close)(

    callback?: () => void

    ): void;

    Gracefully closes the `Http2Session`, allowing any existing streams to complete on their own and preventing new `Http2Stream` instances from being created. Once closed, `http2session.destroy()`*might* be called if there are no open `Http2Stream` instances.

    If specified, the `callback` function is registered as a handler for the`'close'` event.
  + [destroy](https://bun.com/reference/node/http2/Http2Session/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error),

    code?: number

    ): void;

    Immediately terminates the `Http2Session` and the associated `net.Socket` or `tls.TLSSocket`.

    Once destroyed, the `Http2Session` will emit the `'close'` event. If `error` is not undefined, an `'error'` event will be emitted immediately before the `'close'` event.

    If there are any remaining open `Http2Streams` associated with the `Http2Session`, those will also be destroyed.

    @param error

    An `Error` object if the `Http2Session` is being destroyed due to an error.

    @param code

    The HTTP/2 error code to send in the final `GOAWAY` frame. If unspecified, and `error` is not undefined, the default is `INTERNAL_ERROR`, otherwise defaults to `NO_ERROR`.
  + [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'frameError',

    frameType: number,

    errorCode: number,

    streamID: number

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'goaway',

    errorCode: number,

    lastStreamID: number,

    opaqueData?: NonSharedBuffer

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'localSettings',

    settings: [Settings](https://bun.com/reference/node/http2/Settings)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'ping'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'remoteSettings',

    settings: [Settings](https://bun.com/reference/node/http2/Settings)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: 'timeout'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Session/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [eventNames](https://bun.com/reference/node/http2/Http2Session/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2Session/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [goaway](https://bun.com/reference/node/http2/Http2Session/goaway)(

    code?: number,

    lastStreamID?: number,

    opaqueData?: ArrayBufferView<ArrayBufferLike>

    ): void;

    Transmits a `GOAWAY` frame to the connected peer *without* shutting down the`Http2Session`.

    @param code

    An HTTP/2 error code

    @param lastStreamID

    The numeric ID of the last processed `Http2Stream`

    @param opaqueData

    A `TypedArray` or `DataView` instance containing additional data to be carried within the `GOAWAY` frame.
  + [listenerCount](https://bun.com/reference/node/http2/Http2Session/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2Session/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/Http2Session/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number, streamID: number) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'goaway',

    listener: (errorCode: number, lastStreamID: number, opaqueData?: NonSharedBuffer) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'localSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'ping',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'remoteSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: 'timeout',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Session/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number, streamID: number) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'goaway',

    listener: (errorCode: number, lastStreamID: number, opaqueData?: NonSharedBuffer) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'localSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'ping',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'remoteSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: 'timeout',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Session/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [ping](https://bun.com/reference/node/http2/Http2Session/ping)(

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;

    Sends a `PING` frame to the connected HTTP/2 peer. A `callback` function must be provided. The method will return `true` if the `PING` was sent, `false` otherwise.

    The maximum number of outstanding (unacknowledged) pings is determined by the `maxOutstandingPings` configuration option. The default maximum is 10.

    If provided, the `payload` must be a `Buffer`, `TypedArray`, or `DataView` containing 8 bytes of data that will be transmitted with the `PING` and returned with the ping acknowledgment.

    The callback will be invoked with three arguments: an error argument that will be `null` if the `PING` was successfully acknowledged, a `duration` argument that reports the number of milliseconds elapsed since the ping was sent and the acknowledgment was received, and a `Buffer` containing the 8-byte `PING` payload.

    ```
    session.ping(Buffer.from('abcdefgh'), (err, duration, payload) => {
      if (!err) {
        console.log(`Ping acknowledged in ${duration} milliseconds`);
        console.log(`With payload '${payload.toString()}'`);
      }
    });
    ```

    If the `payload` argument is not specified, the default payload will be the 64-bit timestamp (little endian) marking the start of the `PING` duration.

    [ping](https://bun.com/reference/node/http2/Http2Session/ping)(

    payload: ArrayBufferView,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;
  + [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number, streamID: number) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'goaway',

    listener: (errorCode: number, lastStreamID: number, opaqueData?: NonSharedBuffer) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'localSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'ping',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'remoteSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Session/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number, streamID: number) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'goaway',

    listener: (errorCode: number, lastStreamID: number, opaqueData?: NonSharedBuffer) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'localSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'ping',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'remoteSettings',

    listener: (settings: [Settings](https://bun.com/reference/node/http2/Settings)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Session/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/http2/Http2Session/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/http2/Http2Session/ref)(): void;

    Calls `ref()` on this `Http2Session` instance's underlying `net.Socket`.
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2Session/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/Http2Session/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setLocalWindowSize](https://bun.com/reference/node/http2/Http2Session/setLocalWindowSize)(

    windowSize: number

    ): void;

    Sets the local endpoint's window size. The `windowSize` is the total window size to set, not the delta.

    ```
    import http2 from 'node:http2';

    const server = http2.createServer();
    const expectedWindowSize = 2 ** 20;
    server.on('connect', (session) => {

      // Set local window size to be 2 ** 20
      session.setLocalWindowSize(expectedWindowSize);
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2Session/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/Http2Session/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    Used to set a callback function that is called when there is no activity on the `Http2Session` after `msecs` milliseconds. The given `callback` is registered as a listener on the `'timeout'` event.
  + [settings](https://bun.com/reference/node/http2/Http2Session/settings)(

    settings: [Settings](https://bun.com/reference/node/http2/Settings),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), settings: [Settings](https://bun.com/reference/node/http2/Settings), duration: number) => void

    ): void;

    Updates the current local settings for this `Http2Session` and sends a new `SETTINGS` frame to the connected HTTP/2 peer.

    Once called, the `http2session.pendingSettingsAck` property will be `true` while the session is waiting for the remote peer to acknowledge the new settings.

    The new settings will not become effective until the `SETTINGS` acknowledgment is received and the `'localSettings'` event is emitted. It is possible to send multiple `SETTINGS` frames while acknowledgment is still pending.

    @param callback

    Callback that is called once the session is connected or right away if the session is already connected.
  + [unref](https://bun.com/reference/node/http2/Http2Session/unref)(): void;

    Calls `unref()` on this `Http2Session`instance's underlying `net.Socket`.
* ### interface [Http2Stream](https://bun.com/reference/node/http2/Http2Stream)

  Duplex streams are streams that implement both the `Readable` and `Writable` interfaces.

  Examples of `Duplex` streams include:

  + `TCP sockets`
  + `zlib streams`
  + `crypto streams`

  + readonly [aborted](https://bun.com/reference/node/http2/Http2Stream/aborted): boolean

    Set to `true` if the `Http2Stream` instance was aborted abnormally. When set, the `'aborted'` event will have been emitted.
  + [allowHalfOpen](https://bun.com/reference/node/http2/Http2Stream/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bufferSize](https://bun.com/reference/node/http2/Http2Stream/bufferSize): number

    This property shows the number of characters currently buffered to be written. See `net.Socket.bufferSize` for details.
  + readonly [closed](https://bun.com/reference/node/http2/Http2Stream/closed): boolean

    Set to `true` if the `Http2Stream` instance has been closed.
  + readonly [destroyed](https://bun.com/reference/node/http2/Http2Stream/destroyed): boolean

    Set to `true` if the `Http2Stream` instance has been destroyed and is no longer usable.
  + readonly [endAfterHeaders](https://bun.com/reference/node/http2/Http2Stream/endAfterHeaders): boolean

    Set to `true` if the `END_STREAM` flag was set in the request or response HEADERS frame received, indicating that no additional data should be received and the readable side of the `Http2Stream` will be closed.
  + readonly [errored](https://bun.com/reference/node/http2/Http2Stream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [id](https://bun.com/reference/node/http2/Http2Stream/id)?: number

    The numeric stream identifier of this `Http2Stream` instance. Set to `undefined` if the stream identifier has not yet been assigned.
  + readonly [pending](https://bun.com/reference/node/http2/Http2Stream/pending): boolean

    Set to `true` if the `Http2Stream` instance has not yet been assigned a numeric stream identifier.
  + [readable](https://bun.com/reference/node/http2/Http2Stream/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/http2/Http2Stream/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/http2/Http2Stream/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/http2/Http2Stream/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/http2/Http2Stream/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/http2/Http2Stream/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/http2/Http2Stream/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/http2/Http2Stream/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/http2/Http2Stream/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [rstCode](https://bun.com/reference/node/http2/Http2Stream/rstCode): number

    Set to the `RST_STREAM` `error code` reported when the `Http2Stream` is destroyed after either receiving an `RST_STREAM` frame from the connected peer, calling `http2stream.close()`, or `http2stream.destroy()`. Will be `undefined` if the `Http2Stream` has not been closed.
  + readonly [sentHeaders](https://bun.com/reference/node/http2/Http2Stream/sentHeaders): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound headers sent for this `Http2Stream`.
  + readonly [sentInfoHeaders](https://bun.com/reference/node/http2/Http2Stream/sentInfoHeaders)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)[]

    An array of objects containing the outbound informational (additional) headers sent for this `Http2Stream`.
  + readonly [sentTrailers](https://bun.com/reference/node/http2/Http2Stream/sentTrailers)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound trailers sent for this `HttpStream`.
  + readonly [session](https://bun.com/reference/node/http2/Http2Stream/session): undefined | [Http2Session](https://bun.com/reference/node/http2/Http2Session)

    A reference to the `Http2Session` instance that owns this `Http2Stream`. The value will be `undefined` after the `Http2Stream` instance is destroyed.
  + readonly [state](https://bun.com/reference/node/http2/Http2Stream/state): [StreamState](https://bun.com/reference/node/http2/StreamState)

    Provides miscellaneous information about the current state of the `Http2Stream`.

    A current state of this `Http2Stream`.
  + readonly [writable](https://bun.com/reference/node/http2/Http2Stream/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http2/Http2Stream/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http2/Http2Stream/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http2/Http2Stream/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http2/Http2Stream/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http2/Http2Stream/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http2/Http2Stream/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http2/Http2Stream/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http2/Http2Stream/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/http2/Http2Stream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http2/Http2Stream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http2/Http2Stream/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/http2/Http2Stream/_read)(

    size: number

    ): void;
  + [\_write](https://bun.com/reference/node/http2/Http2Stream/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http2/Http2Stream/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/Http2Stream/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/http2/Http2Stream/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/Http2Stream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/Http2Stream/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/http2/Http2Stream/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/http2/Http2Stream/close)(

    code?: number,

    callback?: () => void

    ): void;

    Closes the `Http2Stream` instance by sending an `RST_STREAM` frame to the connected HTTP/2 peer.

    @param code

    Unsigned 32-bit integer identifying the error code.

    @param callback

    An optional function registered to listen for the `'close'` event.
  + [compose](https://bun.com/reference/node/http2/Http2Stream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http2/Http2Stream/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http2/Http2Stream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/http2/Http2Stream/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'aborted'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'data',

    chunk: string | NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'frameError',

    frameType: number,

    errorCode: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'streamClosed',

    code: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'timeout'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'trailers',

    trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: 'wantTrailers'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/Http2Stream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http2/Http2Stream/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http2/Http2Stream/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http2/Http2Stream/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http2/Http2Stream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/http2/Http2Stream/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/http2/Http2Stream/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/http2/Http2Stream/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/http2/Http2Stream/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/http2/Http2Stream/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/http2/Http2Stream/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/http2/Http2Stream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/http2/Http2Stream/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/http2/Http2Stream/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/http2/Http2Stream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/Http2Stream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/http2/Http2Stream/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/http2/Http2Stream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'timeout',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/Http2Stream/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'timeout',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/Http2Stream/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/http2/Http2Stream/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/http2/Http2Stream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/Http2Stream/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/Http2Stream/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/http2/Http2Stream/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/http2/Http2Stream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/http2/Http2Stream/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/http2/Http2Stream/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/http2/Http2Stream/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/http2/Http2Stream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/Http2Stream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/http2/Http2Stream/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [sendTrailers](https://bun.com/reference/node/http2/Http2Stream/sendTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): void;

    Sends a trailing `HEADERS` frame to the connected HTTP/2 peer. This method will cause the `Http2Stream` to be immediately closed and must only be called after the `'wantTrailers'` event has been emitted. When sending a request or sending a response, the `options.waitForTrailers` option must be set in order to keep the `Http2Stream` open after the final `DATA` frame so that trailers can be sent.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond(undefined, { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ xyz: 'abc' });
      });
      stream.end('Hello World');
    });
    ```

    The HTTP/1 specification forbids trailers from containing HTTP/2 pseudo-header fields (e.g. `':method'`, `':path'`, etc).
  + [setDefaultEncoding](https://bun.com/reference/node/http2/Http2Stream/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/http2/Http2Stream/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/http2/Http2Stream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/Http2Stream/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    ```
    import http2 from 'node:http2';
    const client = http2.connect('http://example.org:8000');
    const { NGHTTP2_CANCEL } = http2.constants;
    const req = client.request({ ':path': '/' });

    // Cancel the stream if there's no activity after 5 seconds
    req.setTimeout(5000, () => req.close(NGHTTP2_CANCEL));
    ```
  + [some](https://bun.com/reference/node/http2/Http2Stream/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/http2/Http2Stream/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/http2/Http2Stream/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/http2/Http2Stream/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/http2/Http2Stream/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/http2/Http2Stream/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/http2/Http2Stream/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/http2/Http2Stream/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http2/Http2Stream/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders)

  + [:authority](https://bun.com/reference/node/http2/IncomingHttpHeaders/:authority)?: string
  + [:method](https://bun.com/reference/node/http2/IncomingHttpHeaders/:method)?: string
  + [:path](https://bun.com/reference/node/http2/IncomingHttpHeaders/:path)?: string
  + [:scheme](https://bun.com/reference/node/http2/IncomingHttpHeaders/:scheme)?: string
  + [accept](https://bun.com/reference/node/http2/IncomingHttpHeaders/accept)?: string
  + [accept-encoding](https://bun.com/reference/node/http2/IncomingHttpHeaders/accept-encoding)?: string
  + [accept-language](https://bun.com/reference/node/http2/IncomingHttpHeaders/accept-language)?: string
  + [accept-patch](https://bun.com/reference/node/http2/IncomingHttpHeaders/accept-patch)?: string
  + [accept-ranges](https://bun.com/reference/node/http2/IncomingHttpHeaders/accept-ranges)?: string
  + [access-control-allow-credentials](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-allow-credentials)?: string
  + [access-control-allow-headers](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-allow-headers)?: string
  + [access-control-allow-methods](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-allow-methods)?: string
  + [access-control-allow-origin](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-allow-origin)?: string
  + [access-control-expose-headers](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-expose-headers)?: string
  + [access-control-max-age](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-max-age)?: string
  + [access-control-request-headers](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-request-headers)?: string
  + [access-control-request-method](https://bun.com/reference/node/http2/IncomingHttpHeaders/access-control-request-method)?: string
  + [age](https://bun.com/reference/node/http2/IncomingHttpHeaders/age)?: string
  + [allow](https://bun.com/reference/node/http2/IncomingHttpHeaders/allow)?: string
  + [alt-svc](https://bun.com/reference/node/http2/IncomingHttpHeaders/alt-svc)?: string
  + [authorization](https://bun.com/reference/node/http2/IncomingHttpHeaders/authorization)?: string
  + [cache-control](https://bun.com/reference/node/http2/IncomingHttpHeaders/cache-control)?: string
  + [connection](https://bun.com/reference/node/http2/IncomingHttpHeaders/connection)?: string
  + [content-disposition](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-disposition)?: string
  + [content-encoding](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-encoding)?: string
  + [content-language](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-language)?: string
  + [content-length](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-length)?: string
  + [content-location](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-location)?: string
  + [content-range](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-range)?: string
  + [content-type](https://bun.com/reference/node/http2/IncomingHttpHeaders/content-type)?: string
  + [cookie](https://bun.com/reference/node/http2/IncomingHttpHeaders/cookie)?: string
  + [date](https://bun.com/reference/node/http2/IncomingHttpHeaders/date)?: string
  + [etag](https://bun.com/reference/node/http2/IncomingHttpHeaders/etag)?: string
  + [expect](https://bun.com/reference/node/http2/IncomingHttpHeaders/expect)?: string
  + [expires](https://bun.com/reference/node/http2/IncomingHttpHeaders/expires)?: string
  + [forwarded](https://bun.com/reference/node/http2/IncomingHttpHeaders/forwarded)?: string
  + [from](https://bun.com/reference/node/http2/IncomingHttpHeaders/from)?: string
  + [host](https://bun.com/reference/node/http2/IncomingHttpHeaders/host)?: string
  + [if-match](https://bun.com/reference/node/http2/IncomingHttpHeaders/if-match)?: string
  + [if-modified-since](https://bun.com/reference/node/http2/IncomingHttpHeaders/if-modified-since)?: string
  + [if-none-match](https://bun.com/reference/node/http2/IncomingHttpHeaders/if-none-match)?: string
  + [if-unmodified-since](https://bun.com/reference/node/http2/IncomingHttpHeaders/if-unmodified-since)?: string
  + [last-modified](https://bun.com/reference/node/http2/IncomingHttpHeaders/last-modified)?: string
  + [location](https://bun.com/reference/node/http2/IncomingHttpHeaders/location)?: string
  + [origin](https://bun.com/reference/node/http2/IncomingHttpHeaders/origin)?: string
  + [pragma](https://bun.com/reference/node/http2/IncomingHttpHeaders/pragma)?: string
  + [proxy-authenticate](https://bun.com/reference/node/http2/IncomingHttpHeaders/proxy-authenticate)?: string
  + [proxy-authorization](https://bun.com/reference/node/http2/IncomingHttpHeaders/proxy-authorization)?: string
  + [public-key-pins](https://bun.com/reference/node/http2/IncomingHttpHeaders/public-key-pins)?: string
  + [range](https://bun.com/reference/node/http2/IncomingHttpHeaders/range)?: string
  + [referer](https://bun.com/reference/node/http2/IncomingHttpHeaders/referer)?: string
  + [retry-after](https://bun.com/reference/node/http2/IncomingHttpHeaders/retry-after)?: string
  + [sec-fetch-dest](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-fetch-dest)?: string
  + [sec-fetch-mode](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-fetch-mode)?: string
  + [sec-fetch-site](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-fetch-site)?: string
  + [sec-fetch-user](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-fetch-user)?: string
  + [sec-websocket-accept](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-websocket-accept)?: string
  + [sec-websocket-extensions](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-websocket-extensions)?: string
  + [sec-websocket-key](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-websocket-key)?: string
  + [sec-websocket-version](https://bun.com/reference/node/http2/IncomingHttpHeaders/sec-websocket-version)?: string
  + [set-cookie](https://bun.com/reference/node/http2/IncomingHttpHeaders/set-cookie)?: string[]
  + [strict-transport-security](https://bun.com/reference/node/http2/IncomingHttpHeaders/strict-transport-security)?: string
  + [tk](https://bun.com/reference/node/http2/IncomingHttpHeaders/tk)?: string
  + [trailer](https://bun.com/reference/node/http2/IncomingHttpHeaders/trailer)?: string
  + [transfer-encoding](https://bun.com/reference/node/http2/IncomingHttpHeaders/transfer-encoding)?: string
  + [upgrade](https://bun.com/reference/node/http2/IncomingHttpHeaders/upgrade)?: string
  + [user-agent](https://bun.com/reference/node/http2/IncomingHttpHeaders/user-agent)?: string
  + [vary](https://bun.com/reference/node/http2/IncomingHttpHeaders/vary)?: string
  + [via](https://bun.com/reference/node/http2/IncomingHttpHeaders/via)?: string
  + [warning](https://bun.com/reference/node/http2/IncomingHttpHeaders/warning)?: string
  + [www-authenticate](https://bun.com/reference/node/http2/IncomingHttpHeaders/www-authenticate)?: string
* ### interface [IncomingHttpStatusHeader](https://bun.com/reference/node/http2/IncomingHttpStatusHeader)

  + [:status](https://bun.com/reference/node/http2/IncomingHttpStatusHeader/:status)?: number
* ### interface [SecureClientSessionOptions](https://bun.com/reference/node/http2/SecureClientSessionOptions)

  + [allowPartialTrustChain](https://bun.com/reference/node/http2/SecureClientSessionOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/http2/SecureClientSessionOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [ca](https://bun.com/reference/node/http2/SecureClientSessionOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/http2/SecureClientSessionOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/node/http2/SecureClientSessionOptions/checkServerIdentity)?: (hostname: string, cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)
  + [ciphers](https://bun.com/reference/node/http2/SecureClientSessionOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [createConnection](https://bun.com/reference/node/http2/SecureClientSessionOptions/createConnection)?: (authority: [URL](https://bun.com/reference/node/url/URL), option: [SessionOptions](https://bun.com/reference/node/http2/SessionOptions)) => [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    An optional callback that receives the `URL` instance passed to `connect` and the `options` object, and returns any `Duplex` stream that is to be used as the connection for this session.
  + [crl](https://bun.com/reference/node/http2/SecureClientSessionOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/http2/SecureClientSessionOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/http2/SecureClientSessionOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/http2/SecureClientSessionOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [honorCipherOrder](https://bun.com/reference/node/http2/SecureClientSessionOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [host](https://bun.com/reference/node/http2/SecureClientSessionOptions/host)?: string
  + [key](https://bun.com/reference/node/http2/SecureClientSessionOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [lookup](https://bun.com/reference/node/http2/SecureClientSessionOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxReservedRemoteStreams](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxReservedRemoteStreams)?: number

    Sets the maximum number of reserved push streams the client will accept at any given time. Once the current number of currently reserved push streams exceeds reaches this limit, new push streams sent by the server will be automatically rejected. The minimum allowed value is 0. The maximum allowed value is 2<sup>32</sup>-1. A negative value sets this option to the maximum allowed value.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [maxVersion](https://bun.com/reference/node/http2/SecureClientSessionOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minDHSize](https://bun.com/reference/node/http2/SecureClientSessionOptions/minDHSize)?: number
  + [minVersion](https://bun.com/reference/node/http2/SecureClientSessionOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [paddingStrategy](https://bun.com/reference/node/http2/SecureClientSessionOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [passphrase](https://bun.com/reference/node/http2/SecureClientSessionOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [path](https://bun.com/reference/node/http2/SecureClientSessionOptions/path)?: string
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/SecureClientSessionOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [pfx](https://bun.com/reference/node/http2/SecureClientSessionOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [port](https://bun.com/reference/node/http2/SecureClientSessionOptions/port)?: number
  + [pskCallback](https://bun.com/reference/node/http2/SecureClientSessionOptions/pskCallback)?: (hint: null | string) => null | [PSKCallbackNegotation](https://bun.com/reference/node/tls/PSKCallbackNegotation)

    When negotiating TLS-PSK (pre-shared keys), this function is called with optional identity `hint` provided by the server or `null` in case of TLS 1.3 where `hint` was removed. It will be necessary to provide a custom `tls.checkServerIdentity()` for the connection as the default one will try to check hostname/IP of the server against the certificate but that's not applicable for PSK because there won't be a certificate present. More information can be found in the RFC 4279.
  + [rejectUnauthorized](https://bun.com/reference/node/http2/SecureClientSessionOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/SecureClientSessionOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [requestCert](https://bun.com/reference/node/http2/SecureClientSessionOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/http2/SecureClientSessionOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/http2/SecureClientSessionOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [servername](https://bun.com/reference/node/http2/SecureClientSessionOptions/servername)?: string
  + [session](https://bun.com/reference/node/http2/SecureClientSessionOptions/session)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>
  + [sessionIdContext](https://bun.com/reference/node/http2/SecureClientSessionOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/http2/SecureClientSessionOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [settings](https://bun.com/reference/node/http2/SecureClientSessionOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [sigalgs](https://bun.com/reference/node/http2/SecureClientSessionOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/http2/SecureClientSessionOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [socket](https://bun.com/reference/node/http2/SecureClientSessionOptions/socket)?: [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/SecureClientSessionOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
  + [ticketKeys](https://bun.com/reference/node/http2/SecureClientSessionOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
  + [timeout](https://bun.com/reference/node/http2/SecureClientSessionOptions/timeout)?: number
* ### interface [SecureServerOptions](https://bun.com/reference/node/http2/SecureServerOptions)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  + [allowHalfOpen](https://bun.com/reference/node/http2/SecureServerOptions/allowHalfOpen)?: boolean

    Indicates whether half-opened TCP connections are allowed.
  + [allowHTTP1](https://bun.com/reference/node/http2/SecureServerOptions/allowHTTP1)?: boolean
  + [allowPartialTrustChain](https://bun.com/reference/node/http2/SecureServerOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/http2/SecureServerOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [blockList](https://bun.com/reference/node/http2/SecureServerOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)

    `blockList` can be used for disabling inbound access to specific IP addresses, IP ranges, or IP subnets. This does not work if the server is behind a reverse proxy, NAT, etc. because the address checked against the block list is the address of the proxy, or the one specified by the NAT.
  + [ca](https://bun.com/reference/node/http2/SecureServerOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/http2/SecureServerOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/http2/SecureServerOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/http2/SecureServerOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/http2/SecureServerOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/http2/SecureServerOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/http2/SecureServerOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [handshakeTimeout](https://bun.com/reference/node/http2/SecureServerOptions/handshakeTimeout)?: number

    Abort the connection if the SSL/TLS handshake does not finish in the specified number of milliseconds. A 'tlsClientError' is emitted on the tls.Server object whenever a handshake times out. Default: 120000 (120 seconds).
  + [highWaterMark](https://bun.com/reference/node/http2/SecureServerOptions/highWaterMark)?: number

    Optionally overrides all `net.Socket`s' `readableHighWaterMark` and `writableHighWaterMark`.
  + [honorCipherOrder](https://bun.com/reference/node/http2/SecureServerOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [Http1IncomingMessage](https://bun.com/reference/node/http2/SecureServerOptions/Http1IncomingMessage)?: Http1Request
  + [Http1ServerResponse](https://bun.com/reference/node/http2/SecureServerOptions/Http1ServerResponse)?: Http1Response
  + [Http2ServerRequest](https://bun.com/reference/node/http2/SecureServerOptions/Http2ServerRequest)?: Http2Request
  + [Http2ServerResponse](https://bun.com/reference/node/http2/SecureServerOptions/Http2ServerResponse)?: Http2Response
  + [keepAlive](https://bun.com/reference/node/http2/SecureServerOptions/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/http2/SecureServerOptions/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [key](https://bun.com/reference/node/http2/SecureServerOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/SecureServerOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/SecureServerOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/SecureServerOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/SecureServerOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/SecureServerOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/SecureServerOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [maxVersion](https://bun.com/reference/node/http2/SecureServerOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/http2/SecureServerOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [noDelay](https://bun.com/reference/node/http2/SecureServerOptions/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [origins](https://bun.com/reference/node/http2/SecureServerOptions/origins)?: string[]
  + [paddingStrategy](https://bun.com/reference/node/http2/SecureServerOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [passphrase](https://bun.com/reference/node/http2/SecureServerOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pauseOnConnect](https://bun.com/reference/node/http2/SecureServerOptions/pauseOnConnect)?: boolean

    Indicates whether the socket should be paused on incoming connections.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/SecureServerOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [pfx](https://bun.com/reference/node/http2/SecureServerOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [pskCallback](https://bun.com/reference/node/http2/SecureServerOptions/pskCallback)?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket), identity: string) => null | ArrayBufferView<ArrayBufferLike>
  + [pskIdentityHint](https://bun.com/reference/node/http2/SecureServerOptions/pskIdentityHint)?: string

    hint to send to a client to help with selecting the identity during TLS-PSK negotiation. Will be ignored in TLS 1.3. Upon failing to set pskIdentityHint `tlsClientError` will be emitted with `ERR_TLS_PSK_SET_IDENTIY_HINT_FAILED` code.
  + [rejectUnauthorized](https://bun.com/reference/node/http2/SecureServerOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/SecureServerOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [requestCert](https://bun.com/reference/node/http2/SecureServerOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/http2/SecureServerOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/http2/SecureServerOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [sessionIdContext](https://bun.com/reference/node/http2/SecureServerOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/http2/SecureServerOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [settings](https://bun.com/reference/node/http2/SecureServerOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [sigalgs](https://bun.com/reference/node/http2/SecureServerOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/http2/SecureServerOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [streamResetBurst](https://bun.com/reference/node/http2/SecureServerOptions/streamResetBurst)?: number
  + [streamResetRate](https://bun.com/reference/node/http2/SecureServerOptions/streamResetRate)?: number
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/SecureServerOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
  + [ticketKeys](https://bun.com/reference/node/http2/SecureServerOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data.
* ### interface [SecureServerSessionOptions](https://bun.com/reference/node/http2/SecureServerSessionOptions)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  + [allowHalfOpen](https://bun.com/reference/node/http2/SecureServerSessionOptions/allowHalfOpen)?: boolean

    Indicates whether half-opened TCP connections are allowed.
  + [allowPartialTrustChain](https://bun.com/reference/node/http2/SecureServerSessionOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/http2/SecureServerSessionOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [blockList](https://bun.com/reference/node/http2/SecureServerSessionOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)

    `blockList` can be used for disabling inbound access to specific IP addresses, IP ranges, or IP subnets. This does not work if the server is behind a reverse proxy, NAT, etc. because the address checked against the block list is the address of the proxy, or the one specified by the NAT.
  + [ca](https://bun.com/reference/node/http2/SecureServerSessionOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/http2/SecureServerSessionOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/http2/SecureServerSessionOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/http2/SecureServerSessionOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/http2/SecureServerSessionOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/http2/SecureServerSessionOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/http2/SecureServerSessionOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [handshakeTimeout](https://bun.com/reference/node/http2/SecureServerSessionOptions/handshakeTimeout)?: number

    Abort the connection if the SSL/TLS handshake does not finish in the specified number of milliseconds. A 'tlsClientError' is emitted on the tls.Server object whenever a handshake times out. Default: 120000 (120 seconds).
  + [highWaterMark](https://bun.com/reference/node/http2/SecureServerSessionOptions/highWaterMark)?: number

    Optionally overrides all `net.Socket`s' `readableHighWaterMark` and `writableHighWaterMark`.
  + [honorCipherOrder](https://bun.com/reference/node/http2/SecureServerSessionOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [Http1IncomingMessage](https://bun.com/reference/node/http2/SecureServerSessionOptions/Http1IncomingMessage)?: Http1Request
  + [Http1ServerResponse](https://bun.com/reference/node/http2/SecureServerSessionOptions/Http1ServerResponse)?: Http1Response
  + [Http2ServerRequest](https://bun.com/reference/node/http2/SecureServerSessionOptions/Http2ServerRequest)?: Http2Request
  + [Http2ServerResponse](https://bun.com/reference/node/http2/SecureServerSessionOptions/Http2ServerResponse)?: Http2Response
  + [keepAlive](https://bun.com/reference/node/http2/SecureServerSessionOptions/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/http2/SecureServerSessionOptions/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [key](https://bun.com/reference/node/http2/SecureServerSessionOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [maxVersion](https://bun.com/reference/node/http2/SecureServerSessionOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/http2/SecureServerSessionOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [noDelay](https://bun.com/reference/node/http2/SecureServerSessionOptions/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [paddingStrategy](https://bun.com/reference/node/http2/SecureServerSessionOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [passphrase](https://bun.com/reference/node/http2/SecureServerSessionOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pauseOnConnect](https://bun.com/reference/node/http2/SecureServerSessionOptions/pauseOnConnect)?: boolean

    Indicates whether the socket should be paused on incoming connections.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/SecureServerSessionOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [pfx](https://bun.com/reference/node/http2/SecureServerSessionOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [pskCallback](https://bun.com/reference/node/http2/SecureServerSessionOptions/pskCallback)?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket), identity: string) => null | ArrayBufferView<ArrayBufferLike>
  + [pskIdentityHint](https://bun.com/reference/node/http2/SecureServerSessionOptions/pskIdentityHint)?: string

    hint to send to a client to help with selecting the identity during TLS-PSK negotiation. Will be ignored in TLS 1.3. Upon failing to set pskIdentityHint `tlsClientError` will be emitted with `ERR_TLS_PSK_SET_IDENTIY_HINT_FAILED` code.
  + [rejectUnauthorized](https://bun.com/reference/node/http2/SecureServerSessionOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/SecureServerSessionOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [requestCert](https://bun.com/reference/node/http2/SecureServerSessionOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/http2/SecureServerSessionOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/http2/SecureServerSessionOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [sessionIdContext](https://bun.com/reference/node/http2/SecureServerSessionOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/http2/SecureServerSessionOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [settings](https://bun.com/reference/node/http2/SecureServerSessionOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [sigalgs](https://bun.com/reference/node/http2/SecureServerSessionOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/http2/SecureServerSessionOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [streamResetBurst](https://bun.com/reference/node/http2/SecureServerSessionOptions/streamResetBurst)?: number
  + [streamResetRate](https://bun.com/reference/node/http2/SecureServerSessionOptions/streamResetRate)?: number
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/SecureServerSessionOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
  + [ticketKeys](https://bun.com/reference/node/http2/SecureServerSessionOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data.
* ### interface [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + readonly [closed](https://bun.com/reference/node/http2/ServerHttp2Session/closed): boolean

    Will be `true` if this `Http2Session` instance has been closed, otherwise `false`.
  + readonly [connecting](https://bun.com/reference/node/http2/ServerHttp2Session/connecting): boolean

    Will be `true` if this `Http2Session` instance is still connecting, will be set to `false` before emitting `connect` event and/or calling the `http2.connect` callback.
  + readonly [destroyed](https://bun.com/reference/node/http2/ServerHttp2Session/destroyed): boolean

    Will be `true` if this `Http2Session` instance has been destroyed and must no longer be used, otherwise `false`.
  + readonly [encrypted](https://bun.com/reference/node/http2/ServerHttp2Session/encrypted)?: boolean

    Value is `undefined` if the `Http2Session` session socket has not yet been connected, `true` if the `Http2Session` is connected with a `TLSSocket`, and `false` if the `Http2Session` is connected to any other kind of socket or stream.
  + readonly [localSettings](https://bun.com/reference/node/http2/ServerHttp2Session/localSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current local settings of this `Http2Session`. The local settings are local to *this*`Http2Session` instance.
  + readonly [originSet](https://bun.com/reference/node/http2/ServerHttp2Session/originSet)?: string[]

    If the `Http2Session` is connected to a `TLSSocket`, the `originSet` property will return an `Array` of origins for which the `Http2Session` may be considered authoritative.

    The `originSet` property is only available when using a secure TLS connection.
  + readonly [pendingSettingsAck](https://bun.com/reference/node/http2/ServerHttp2Session/pendingSettingsAck): boolean

    Indicates whether the `Http2Session` is currently waiting for acknowledgment of a sent `SETTINGS` frame. Will be `true` after calling the `http2session.settings()` method. Will be `false` once all sent `SETTINGS` frames have been acknowledged.
  + readonly [remoteSettings](https://bun.com/reference/node/http2/ServerHttp2Session/remoteSettings): [Settings](https://bun.com/reference/node/http2/Settings)

    A prototype-less object describing the current remote settings of this`Http2Session`. The remote settings are set by the *connected* HTTP/2 peer.
  + readonly [server](https://bun.com/reference/node/http2/ServerHttp2Session/server): [Http2Server](https://bun.com/reference/node/http2/Http2Server)<Http1Request, Http1Response, Http2Request, Http2Response> | [Http2SecureServer](https://bun.com/reference/node/http2/Http2SecureServer)<Http1Request, Http1Response, Http2Request, Http2Response>
  + readonly [socket](https://bun.com/reference/node/http2/ServerHttp2Session/socket): [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    Returns a `Proxy` object that acts as a `net.Socket` (or `tls.TLSSocket`) but limits available methods to ones safe to use with HTTP/2.

    `destroy`, `emit`, `end`, `pause`, `read`, `resume`, and `write` will throw an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See `Http2Session and Sockets` for more information.

    `setTimeout` method will be called on this `Http2Session`.

    All other interactions will be routed directly to the socket.
  + readonly [state](https://bun.com/reference/node/http2/ServerHttp2Session/state): [SessionState](https://bun.com/reference/node/http2/SessionState)

    Provides miscellaneous information about the current state of the`Http2Session`.

    An object describing the current status of this `Http2Session`.
  + readonly [type](https://bun.com/reference/node/http2/ServerHttp2Session/type): number

    The `http2session.type` will be equal to `http2.constants.NGHTTP2_SESSION_SERVER` if this `Http2Session` instance is a server, and `http2.constants.NGHTTP2_SESSION_CLIENT` if the instance is a client.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/ServerHttp2Session/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http2/ServerHttp2Session/addListener)(

    event: 'connect',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>, socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Session/addListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Session/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [altsvc](https://bun.com/reference/node/http2/ServerHttp2Session/altsvc)(

    alt: string,

    originOrStream: string | number | [URL](https://bun.com/reference/node/url/URL) | [AlternativeServiceOptions](https://bun.com/reference/node/http2/AlternativeServiceOptions)

    ): void;

    Submits an `ALTSVC` frame (as defined by [RFC 7838](https://tools.ietf.org/html/rfc7838)) to the connected client.

    ```
    import http2 from 'node:http2';

    const server = http2.createServer();
    server.on('session', (session) => {
      // Set altsvc for origin https://example.org:80
      session.altsvc('h2=":8000"', 'https://example.org:80');
    });

    server.on('stream', (stream) => {
      // Set altsvc for a specific stream
      stream.session.altsvc('h2=":8000"', stream.id);
    });
    ```

    Sending an `ALTSVC` frame with a specific stream ID indicates that the alternate service is associated with the origin of the given `Http2Stream`.

    The `alt` and origin string *must* contain only ASCII bytes and are strictly interpreted as a sequence of ASCII bytes. The special value `'clear'`may be passed to clear any previously set alternative service for a given domain.

    When a string is passed for the `originOrStream` argument, it will be parsed as a URL and the origin will be derived. For instance, the origin for the HTTP URL `'https://example.org/foo/bar'` is the ASCII string`'https://example.org'`. An error will be thrown if either the given string cannot be parsed as a URL or if a valid origin cannot be derived.

    A `URL` object, or any object with an `origin` property, may be passed as`originOrStream`, in which case the value of the `origin` property will be used. The value of the `origin` property *must* be a properly serialized ASCII origin.

    @param alt

    A description of the alternative service configuration as defined by `RFC 7838`.

    @param originOrStream

    Either a URL string specifying the origin (or an `Object` with an `origin` property) or the numeric identifier of an active `Http2Stream` as given by the `http2stream.id` property.
  + [close](https://bun.com/reference/node/http2/ServerHttp2Session/close)(

    callback?: () => void

    ): void;

    Gracefully closes the `Http2Session`, allowing any existing streams to complete on their own and preventing new `Http2Stream` instances from being created. Once closed, `http2session.destroy()`*might* be called if there are no open `Http2Stream` instances.

    If specified, the `callback` function is registered as a handler for the`'close'` event.
  + [destroy](https://bun.com/reference/node/http2/ServerHttp2Session/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error),

    code?: number

    ): void;

    Immediately terminates the `Http2Session` and the associated `net.Socket` or `tls.TLSSocket`.

    Once destroyed, the `Http2Session` will emit the `'close'` event. If `error` is not undefined, an `'error'` event will be emitted immediately before the `'close'` event.

    If there are any remaining open `Http2Streams` associated with the `Http2Session`, those will also be destroyed.

    @param error

    An `Error` object if the `Http2Session` is being destroyed due to an error.

    @param code

    The HTTP/2 error code to send in the final `GOAWAY` frame. If unspecified, and `error` is not undefined, the default is `INTERNAL_ERROR`, otherwise defaults to `NO_ERROR`.
  + [emit](https://bun.com/reference/node/http2/ServerHttp2Session/emit)(

    event: 'connect',

    session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>,

    socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ServerHttp2Session/emit)(

    event: 'stream',

    stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream),

    headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number,

    rawHeaders: string[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ServerHttp2Session/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [eventNames](https://bun.com/reference/node/http2/ServerHttp2Session/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/http2/ServerHttp2Session/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [goaway](https://bun.com/reference/node/http2/ServerHttp2Session/goaway)(

    code?: number,

    lastStreamID?: number,

    opaqueData?: ArrayBufferView<ArrayBufferLike>

    ): void;

    Transmits a `GOAWAY` frame to the connected peer *without* shutting down the`Http2Session`.

    @param code

    An HTTP/2 error code

    @param lastStreamID

    The numeric ID of the last processed `Http2Stream`

    @param opaqueData

    A `TypedArray` or `DataView` instance containing additional data to be carried within the `GOAWAY` frame.
  + [listenerCount](https://bun.com/reference/node/http2/ServerHttp2Session/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/ServerHttp2Session/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/http2/ServerHttp2Session/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/ServerHttp2Session/on)(

    event: 'connect',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>, socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ServerHttp2Session/on)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ServerHttp2Session/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/http2/ServerHttp2Session/once)(

    event: 'connect',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>, socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ServerHttp2Session/once)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ServerHttp2Session/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [origin](https://bun.com/reference/node/http2/ServerHttp2Session/origin)(

    ...origins: string | [URL](https://bun.com/reference/node/url/URL) | { origin: string }[]

    ): void;

    Submits an `ORIGIN` frame (as defined by [RFC 8336](https://tools.ietf.org/html/rfc8336)) to the connected client to advertise the set of origins for which the server is capable of providing authoritative responses.

    ```
    import http2 from 'node:http2';
    const options = getSecureOptionsSomehow();
    const server = http2.createSecureServer(options);
    server.on('stream', (stream) => {
      stream.respond();
      stream.end('ok');
    });
    server.on('session', (session) => {
      session.origin('https://example.com', 'https://example.org');
    });
    ```

    When a string is passed as an `origin`, it will be parsed as a URL and the origin will be derived. For instance, the origin for the HTTP URL `'https://example.org/foo/bar'` is the ASCII string `'https://example.org'`. An error will be thrown if either the given string cannot be parsed as a URL or if a valid origin cannot be derived.

    A `URL` object, or any object with an `origin` property, may be passed as an `origin`, in which case the value of the `origin` property will be used. The value of the `origin` property *must* be a properly serialized ASCII origin.

    Alternatively, the `origins` option may be used when creating a new HTTP/2 server using the `http2.createSecureServer()` method:

    ```
    import http2 from 'node:http2';
    const options = getSecureOptionsSomehow();
    options.origins = ['https://example.com', 'https://example.org'];
    const server = http2.createSecureServer(options);
    server.on('stream', (stream) => {
      stream.respond();
      stream.end('ok');
    });
    ```

    @param origins

    One or more URL Strings passed as separate arguments.
  + [ping](https://bun.com/reference/node/http2/ServerHttp2Session/ping)(

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;

    Sends a `PING` frame to the connected HTTP/2 peer. A `callback` function must be provided. The method will return `true` if the `PING` was sent, `false` otherwise.

    The maximum number of outstanding (unacknowledged) pings is determined by the `maxOutstandingPings` configuration option. The default maximum is 10.

    If provided, the `payload` must be a `Buffer`, `TypedArray`, or `DataView` containing 8 bytes of data that will be transmitted with the `PING` and returned with the ping acknowledgment.

    The callback will be invoked with three arguments: an error argument that will be `null` if the `PING` was successfully acknowledged, a `duration` argument that reports the number of milliseconds elapsed since the ping was sent and the acknowledgment was received, and a `Buffer` containing the 8-byte `PING` payload.

    ```
    session.ping(Buffer.from('abcdefgh'), (err, duration, payload) => {
      if (!err) {
        console.log(`Ping acknowledged in ${duration} milliseconds`);
        console.log(`With payload '${payload.toString()}'`);
      }
    });
    ```

    If the `payload` argument is not specified, the default payload will be the 64-bit timestamp (little endian) marking the start of the `PING` duration.

    [ping](https://bun.com/reference/node/http2/ServerHttp2Session/ping)(

    payload: ArrayBufferView,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), duration: number, payload: NonSharedBuffer) => void

    ): boolean;
  + [prependListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependListener)(

    event: 'connect',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>, socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependOnceListener)(

    event: 'connect',

    listener: (session: [ServerHttp2Session](https://bun.com/reference/node/http2/ServerHttp2Session)<Http1Request, Http1Response, Http2Request, Http2Response>, socket: [Socket](https://bun.com/reference/node/net/Socket) | [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependOnceListener)(

    event: 'stream',

    listener: (stream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number, rawHeaders: string[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Session/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/http2/ServerHttp2Session/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/http2/ServerHttp2Session/ref)(): void;

    Calls `ref()` on this `Http2Session` instance's underlying `net.Socket`.
  + [removeAllListeners](https://bun.com/reference/node/http2/ServerHttp2Session/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/ServerHttp2Session/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setLocalWindowSize](https://bun.com/reference/node/http2/ServerHttp2Session/setLocalWindowSize)(

    windowSize: number

    ): void;

    Sets the local endpoint's window size. The `windowSize` is the total window size to set, not the delta.

    ```
    import http2 from 'node:http2';

    const server = http2.createServer();
    const expectedWindowSize = 2 ** 20;
    server.on('connect', (session) => {

      // Set local window size to be 2 ** 20
      session.setLocalWindowSize(expectedWindowSize);
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http2/ServerHttp2Session/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/ServerHttp2Session/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    Used to set a callback function that is called when there is no activity on the `Http2Session` after `msecs` milliseconds. The given `callback` is registered as a listener on the `'timeout'` event.
  + [settings](https://bun.com/reference/node/http2/ServerHttp2Session/settings)(

    settings: [Settings](https://bun.com/reference/node/http2/Settings),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), settings: [Settings](https://bun.com/reference/node/http2/Settings), duration: number) => void

    ): void;

    Updates the current local settings for this `Http2Session` and sends a new `SETTINGS` frame to the connected HTTP/2 peer.

    Once called, the `http2session.pendingSettingsAck` property will be `true` while the session is waiting for the remote peer to acknowledge the new settings.

    The new settings will not become effective until the `SETTINGS` acknowledgment is received and the `'localSettings'` event is emitted. It is possible to send multiple `SETTINGS` frames while acknowledgment is still pending.

    @param callback

    Callback that is called once the session is connected or right away if the session is already connected.
  + [unref](https://bun.com/reference/node/http2/ServerHttp2Session/unref)(): void;

    Calls `unref()` on this `Http2Session`instance's underlying `net.Socket`.
* ### interface [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream)

  Duplex streams are streams that implement both the `Readable` and `Writable` interfaces.

  Examples of `Duplex` streams include:

  + `TCP sockets`
  + `zlib streams`
  + `crypto streams`

  + readonly [aborted](https://bun.com/reference/node/http2/ServerHttp2Stream/aborted): boolean

    Set to `true` if the `Http2Stream` instance was aborted abnormally. When set, the `'aborted'` event will have been emitted.
  + [allowHalfOpen](https://bun.com/reference/node/http2/ServerHttp2Stream/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bufferSize](https://bun.com/reference/node/http2/ServerHttp2Stream/bufferSize): number

    This property shows the number of characters currently buffered to be written. See `net.Socket.bufferSize` for details.
  + readonly [closed](https://bun.com/reference/node/http2/ServerHttp2Stream/closed): boolean

    Set to `true` if the `Http2Stream` instance has been closed.
  + readonly [destroyed](https://bun.com/reference/node/http2/ServerHttp2Stream/destroyed): boolean

    Set to `true` if the `Http2Stream` instance has been destroyed and is no longer usable.
  + readonly [endAfterHeaders](https://bun.com/reference/node/http2/ServerHttp2Stream/endAfterHeaders): boolean

    Set to `true` if the `END_STREAM` flag was set in the request or response HEADERS frame received, indicating that no additional data should be received and the readable side of the `Http2Stream` will be closed.
  + readonly [errored](https://bun.com/reference/node/http2/ServerHttp2Stream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headersSent](https://bun.com/reference/node/http2/ServerHttp2Stream/headersSent): boolean

    True if headers were sent, false otherwise (read-only).
  + readonly [id](https://bun.com/reference/node/http2/ServerHttp2Stream/id)?: number

    The numeric stream identifier of this `Http2Stream` instance. Set to `undefined` if the stream identifier has not yet been assigned.
  + readonly [pending](https://bun.com/reference/node/http2/ServerHttp2Stream/pending): boolean

    Set to `true` if the `Http2Stream` instance has not yet been assigned a numeric stream identifier.
  + readonly [pushAllowed](https://bun.com/reference/node/http2/ServerHttp2Stream/pushAllowed): boolean

    Read-only property mapped to the `SETTINGS_ENABLE_PUSH` flag of the remote client's most recent `SETTINGS` frame. Will be `true` if the remote peer accepts push streams, `false` otherwise. Settings are the same for every `Http2Stream` in the same `Http2Session`.
  + [readable](https://bun.com/reference/node/http2/ServerHttp2Stream/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/http2/ServerHttp2Stream/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/http2/ServerHttp2Stream/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/http2/ServerHttp2Stream/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/http2/ServerHttp2Stream/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/http2/ServerHttp2Stream/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/http2/ServerHttp2Stream/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/http2/ServerHttp2Stream/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/http2/ServerHttp2Stream/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [rstCode](https://bun.com/reference/node/http2/ServerHttp2Stream/rstCode): number

    Set to the `RST_STREAM` `error code` reported when the `Http2Stream` is destroyed after either receiving an `RST_STREAM` frame from the connected peer, calling `http2stream.close()`, or `http2stream.destroy()`. Will be `undefined` if the `Http2Stream` has not been closed.
  + readonly [sentHeaders](https://bun.com/reference/node/http2/ServerHttp2Stream/sentHeaders): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound headers sent for this `Http2Stream`.
  + readonly [sentInfoHeaders](https://bun.com/reference/node/http2/ServerHttp2Stream/sentInfoHeaders)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)[]

    An array of objects containing the outbound informational (additional) headers sent for this `Http2Stream`.
  + readonly [sentTrailers](https://bun.com/reference/node/http2/ServerHttp2Stream/sentTrailers)?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    An object containing the outbound trailers sent for this `HttpStream`.
  + readonly [session](https://bun.com/reference/node/http2/ServerHttp2Stream/session): undefined | [Http2Session](https://bun.com/reference/node/http2/Http2Session)

    A reference to the `Http2Session` instance that owns this `Http2Stream`. The value will be `undefined` after the `Http2Stream` instance is destroyed.
  + readonly [state](https://bun.com/reference/node/http2/ServerHttp2Stream/state): [StreamState](https://bun.com/reference/node/http2/StreamState)

    Provides miscellaneous information about the current state of the `Http2Stream`.

    A current state of this `Http2Stream`.
  + readonly [writable](https://bun.com/reference/node/http2/ServerHttp2Stream/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http2/ServerHttp2Stream/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http2/ServerHttp2Stream/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http2/ServerHttp2Stream/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http2/ServerHttp2Stream/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http2/ServerHttp2Stream/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http2/ServerHttp2Stream/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http2/ServerHttp2Stream/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http2/ServerHttp2Stream/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/http2/ServerHttp2Stream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http2/ServerHttp2Stream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http2/ServerHttp2Stream/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/http2/ServerHttp2Stream/_read)(

    size: number

    ): void;
  + [\_write](https://bun.com/reference/node/http2/ServerHttp2Stream/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http2/ServerHttp2Stream/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http2/ServerHttp2Stream/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/http2/ServerHttp2Stream/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http2/ServerHttp2Stream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [additionalHeaders](https://bun.com/reference/node/http2/ServerHttp2Stream/additionalHeaders)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): void;

    Sends an additional informational `HEADERS` frame to the connected HTTP/2 peer.
  + [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/http2/ServerHttp2Stream/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/http2/ServerHttp2Stream/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/http2/ServerHttp2Stream/close)(

    code?: number,

    callback?: () => void

    ): void;

    Closes the `Http2Stream` instance by sending an `RST_STREAM` frame to the connected HTTP/2 peer.

    @param code

    Unsigned 32-bit integer identifying the error code.

    @param callback

    An optional function registered to listen for the `'close'` event.
  + [compose](https://bun.com/reference/node/http2/ServerHttp2Stream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http2/ServerHttp2Stream/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http2/ServerHttp2Stream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/http2/ServerHttp2Stream/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'aborted'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'data',

    chunk: string | NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'frameError',

    frameType: number,

    errorCode: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'streamClosed',

    code: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'timeout'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'trailers',

    trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders),

    flags: number

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: 'wantTrailers'

    ): boolean;

    [emit](https://bun.com/reference/node/http2/ServerHttp2Stream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http2/ServerHttp2Stream/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http2/ServerHttp2Stream/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http2/ServerHttp2Stream/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http2/ServerHttp2Stream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/http2/ServerHttp2Stream/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/http2/ServerHttp2Stream/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/http2/ServerHttp2Stream/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/http2/ServerHttp2Stream/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/http2/ServerHttp2Stream/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/http2/ServerHttp2Stream/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/http2/ServerHttp2Stream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/http2/ServerHttp2Stream/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/http2/ServerHttp2Stream/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/http2/ServerHttp2Stream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http2/ServerHttp2Stream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/http2/ServerHttp2Stream/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/http2/ServerHttp2Stream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'timeout',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http2/ServerHttp2Stream/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'timeout',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http2/ServerHttp2Stream/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/http2/ServerHttp2Stream/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/http2/ServerHttp2Stream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'aborted',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'data',

    listener: (chunk: string | NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'frameError',

    listener: (frameType: number, errorCode: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'streamClosed',

    listener: (code: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'trailers',

    listener: (trailers: [IncomingHttpHeaders](https://bun.com/reference/node/http2/IncomingHttpHeaders), flags: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: 'wantTrailers',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http2/ServerHttp2Stream/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/http2/ServerHttp2Stream/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [pushStream](https://bun.com/reference/node/http2/ServerHttp2Stream/pushStream)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), pushStream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)) => void

    ): void;

    Initiates a push stream. The callback is invoked with the new `Http2Stream` instance created for the push stream passed as the second argument, or an `Error` passed as the first argument.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond({ ':status': 200 });
      stream.pushStream({ ':path': '/' }, (err, pushStream, headers) => {
        if (err) throw err;
        pushStream.respond({ ':status': 200 });
        pushStream.end('some pushed data');
      });
      stream.end('some data');
    });
    ```

    Setting the weight of a push stream is not allowed in the `HEADERS` frame. Pass a `weight` value to `http2stream.priority` with the `silent` option set to `true` to enable server-side bandwidth balancing between concurrent streams.

    Calling `http2stream.pushStream()` from within a pushed stream is not permitted and will throw an error.

    @param callback

    Callback that is called once the push stream has been initiated.

    [pushStream](https://bun.com/reference/node/http2/ServerHttp2Stream/pushStream)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    options?: Pick<[ClientSessionRequestOptions](https://bun.com/reference/node/http2/ClientSessionRequestOptions), 'exclusive' | 'parent'>,

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), pushStream: [ServerHttp2Stream](https://bun.com/reference/node/http2/ServerHttp2Stream), headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)) => void

    ): void;
  + [rawListeners](https://bun.com/reference/node/http2/ServerHttp2Stream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/http2/ServerHttp2Stream/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/http2/ServerHttp2Stream/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/http2/ServerHttp2Stream/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/http2/ServerHttp2Stream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http2/ServerHttp2Stream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [respond](https://bun.com/reference/node/http2/ServerHttp2Stream/respond)(

    headers?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    options?: [ServerStreamResponseOptions](https://bun.com/reference/node/http2/ServerStreamResponseOptions)

    ): void;

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond({ ':status': 200 });
      stream.end('some data');
    });
    ```

    Initiates a response. When the `options.waitForTrailers` option is set, the `'wantTrailers'` event will be emitted immediately after queuing the last chunk of payload data to be sent. The `http2stream.sendTrailers()` method can then be used to send trailing header fields to the peer.

    When `options.waitForTrailers` is set, the `Http2Stream` will not automatically close when the final `DATA` frame is transmitted. User code must call either `http2stream.sendTrailers()` or `http2stream.close()` to close the `Http2Stream`.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond({ ':status': 200 }, { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ ABC: 'some value to send' });
      });
      stream.end('some data');
    });
    ```
  + [respondWithFD](https://bun.com/reference/node/http2/ServerHttp2Stream/respondWithFD)(

    fd: number | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

    headers?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    options?: [ServerStreamFileResponseOptions](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions)

    ): void;

    Initiates a response whose data is read from the given file descriptor. No validation is performed on the given file descriptor. If an error occurs while attempting to read data using the file descriptor, the `Http2Stream` will be closed using an `RST_STREAM` frame using the standard `INTERNAL_ERROR` code.

    When used, the `Http2Stream` object's `Duplex` interface will be closed automatically.

    ```
    import http2 from 'node:http2';
    import fs from 'node:fs';

    const server = http2.createServer();
    server.on('stream', (stream) => {
      const fd = fs.openSync('/some/file', 'r');

      const stat = fs.fstatSync(fd);
      const headers = {
        'content-length': stat.size,
        'last-modified': stat.mtime.toUTCString(),
        'content-type': 'text/plain; charset=utf-8',
      };
      stream.respondWithFD(fd, headers);
      stream.on('close', () => fs.closeSync(fd));
    });
    ```

    The optional `options.statCheck` function may be specified to give user code an opportunity to set additional content headers based on the `fs.Stat` details of the given fd. If the `statCheck` function is provided, the `http2stream.respondWithFD()` method will perform an `fs.fstat()` call to collect details on the provided file descriptor.

    The `offset` and `length` options may be used to limit the response to a specific range subset. This can be used, for instance, to support HTTP Range requests.

    The file descriptor or `FileHandle` is not closed when the stream is closed, so it will need to be closed manually once it is no longer needed. Using the same file descriptor concurrently for multiple streams is not supported and may result in data loss. Re-using a file descriptor after a stream has finished is supported.

    When the `options.waitForTrailers` option is set, the `'wantTrailers'` event will be emitted immediately after queuing the last chunk of payload data to be sent. The `http2stream.sendTrailers()` method can then be used to sent trailing header fields to the peer.

    When `options.waitForTrailers` is set, the `Http2Stream` will not automatically close when the final `DATA` frame is transmitted. User code *must* call either `http2stream.sendTrailers()` or `http2stream.close()` to close the `Http2Stream`.

    ```
    import http2 from 'node:http2';
    import fs from 'node:fs';

    const server = http2.createServer();
    server.on('stream', (stream) => {
      const fd = fs.openSync('/some/file', 'r');

      const stat = fs.fstatSync(fd);
      const headers = {
        'content-length': stat.size,
        'last-modified': stat.mtime.toUTCString(),
        'content-type': 'text/plain; charset=utf-8',
      };
      stream.respondWithFD(fd, headers, { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ ABC: 'some value to send' });
      });

      stream.on('close', () => fs.closeSync(fd));
    });
    ```

    @param fd

    A readable file descriptor.
  + [respondWithFile](https://bun.com/reference/node/http2/ServerHttp2Stream/respondWithFile)(

    path: string,

    headers?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders),

    options?: [ServerStreamFileResponseOptionsWithError](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError)

    ): void;

    Sends a regular file as the response. The `path` must specify a regular file or an `'error'` event will be emitted on the `Http2Stream` object.

    When used, the `Http2Stream` object's `Duplex` interface will be closed automatically.

    The optional `options.statCheck` function may be specified to give user code an opportunity to set additional content headers based on the `fs.Stat` details of the given file:

    If an error occurs while attempting to read the file data, the `Http2Stream` will be closed using an `RST_STREAM` frame using the standard `INTERNAL_ERROR` code. If the `onError` callback is defined, then it will be called. Otherwise, the stream will be destroyed.

    Example using a file path:

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      function statCheck(stat, headers) {
        headers['last-modified'] = stat.mtime.toUTCString();
      }

      function onError(err) {
        // stream.respond() can throw if the stream has been destroyed by
        // the other side.
        try {
          if (err.code === 'ENOENT') {
            stream.respond({ ':status': 404 });
          } else {
            stream.respond({ ':status': 500 });
          }
        } catch (err) {
          // Perform actual error handling.
          console.error(err);
        }
        stream.end();
      }

      stream.respondWithFile('/some/file',
                             { 'content-type': 'text/plain; charset=utf-8' },
                             { statCheck, onError });
    });
    ```

    The `options.statCheck` function may also be used to cancel the send operation by returning `false`. For instance, a conditional request may check the stat results to determine if the file has been modified to return an appropriate `304` response:

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      function statCheck(stat, headers) {
        // Check the stat here...
        stream.respond({ ':status': 304 });
        return false; // Cancel the send operation
      }
      stream.respondWithFile('/some/file',
                             { 'content-type': 'text/plain; charset=utf-8' },
                             { statCheck });
    });
    ```

    The `content-length` header field will be automatically set.

    The `offset` and `length` options may be used to limit the response to a specific range subset. This can be used, for instance, to support HTTP Range requests.

    The `options.onError` function may also be used to handle all the errors that could happen before the delivery of the file is initiated. The default behavior is to destroy the stream.

    When the `options.waitForTrailers` option is set, the `'wantTrailers'` event will be emitted immediately after queuing the last chunk of payload data to be sent. The `http2stream.sendTrailers()` method can then be used to sent trailing header fields to the peer.

    When `options.waitForTrailers` is set, the `Http2Stream` will not automatically close when the final `DATA` frame is transmitted. User code must call either`http2stream.sendTrailers()` or `http2stream.close()` to close the`Http2Stream`.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respondWithFile('/some/file',
                             { 'content-type': 'text/plain; charset=utf-8' },
                             { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ ABC: 'some value to send' });
      });
    });
    ```
  + [resume](https://bun.com/reference/node/http2/ServerHttp2Stream/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [sendTrailers](https://bun.com/reference/node/http2/ServerHttp2Stream/sendTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

    ): void;

    Sends a trailing `HEADERS` frame to the connected HTTP/2 peer. This method will cause the `Http2Stream` to be immediately closed and must only be called after the `'wantTrailers'` event has been emitted. When sending a request or sending a response, the `options.waitForTrailers` option must be set in order to keep the `Http2Stream` open after the final `DATA` frame so that trailers can be sent.

    ```
    import http2 from 'node:http2';
    const server = http2.createServer();
    server.on('stream', (stream) => {
      stream.respond(undefined, { waitForTrailers: true });
      stream.on('wantTrailers', () => {
        stream.sendTrailers({ xyz: 'abc' });
      });
      stream.end('Hello World');
    });
    ```

    The HTTP/1 specification forbids trailers from containing HTTP/2 pseudo-header fields (e.g. `':method'`, `':path'`, etc).
  + [setDefaultEncoding](https://bun.com/reference/node/http2/ServerHttp2Stream/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/http2/ServerHttp2Stream/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/http2/ServerHttp2Stream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http2/ServerHttp2Stream/setTimeout)(

    msecs: number,

    callback?: () => void

    ): void;

    ```
    import http2 from 'node:http2';
    const client = http2.connect('http://example.org:8000');
    const { NGHTTP2_CANCEL } = http2.constants;
    const req = client.request({ ':path': '/' });

    // Cancel the stream if there's no activity after 5 seconds
    req.setTimeout(5000, () => req.close(NGHTTP2_CANCEL));
    ```
  + [some](https://bun.com/reference/node/http2/ServerHttp2Stream/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/http2/ServerHttp2Stream/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/http2/ServerHttp2Stream/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/http2/ServerHttp2Stream/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/http2/ServerHttp2Stream/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/http2/ServerHttp2Stream/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/http2/ServerHttp2Stream/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/http2/ServerHttp2Stream/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http2/ServerHttp2Stream/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [ServerOptions](https://bun.com/reference/node/http2/ServerOptions)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  + [Http1IncomingMessage](https://bun.com/reference/node/http2/ServerOptions/Http1IncomingMessage)?: Http1Request
  + [Http1ServerResponse](https://bun.com/reference/node/http2/ServerOptions/Http1ServerResponse)?: Http1Response
  + [Http2ServerRequest](https://bun.com/reference/node/http2/ServerOptions/Http2ServerRequest)?: Http2Request
  + [Http2ServerResponse](https://bun.com/reference/node/http2/ServerOptions/Http2ServerResponse)?: Http2Response
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/ServerOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/ServerOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/ServerOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/ServerOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/ServerOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/ServerOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [paddingStrategy](https://bun.com/reference/node/http2/ServerOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/ServerOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/ServerOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [settings](https://bun.com/reference/node/http2/ServerOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [streamResetBurst](https://bun.com/reference/node/http2/ServerOptions/streamResetBurst)?: number
  + [streamResetRate](https://bun.com/reference/node/http2/ServerOptions/streamResetRate)?: number
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/ServerOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
* ### interface [ServerSessionOptions](https://bun.com/reference/node/http2/ServerSessionOptions)<Http1Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Http1Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse), Http2Request extends typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest) = typeof [Http2ServerRequest](https://bun.com/reference/node/http2/Http2ServerRequest), Http2Response extends typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse) = typeof [Http2ServerResponse](https://bun.com/reference/node/http2/Http2ServerResponse)>

  + [Http1IncomingMessage](https://bun.com/reference/node/http2/ServerSessionOptions/Http1IncomingMessage)?: Http1Request
  + [Http1ServerResponse](https://bun.com/reference/node/http2/ServerSessionOptions/Http1ServerResponse)?: Http1Response
  + [Http2ServerRequest](https://bun.com/reference/node/http2/ServerSessionOptions/Http2ServerRequest)?: Http2Request
  + [Http2ServerResponse](https://bun.com/reference/node/http2/ServerSessionOptions/Http2ServerResponse)?: Http2Response
  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/ServerSessionOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/ServerSessionOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/ServerSessionOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/ServerSessionOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/ServerSessionOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/ServerSessionOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [paddingStrategy](https://bun.com/reference/node/http2/ServerSessionOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/ServerSessionOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/ServerSessionOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [settings](https://bun.com/reference/node/http2/ServerSessionOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [streamResetBurst](https://bun.com/reference/node/http2/ServerSessionOptions/streamResetBurst)?: number
  + [streamResetRate](https://bun.com/reference/node/http2/ServerSessionOptions/streamResetRate)?: number
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/ServerSessionOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
* ### interface [ServerStreamFileResponseOptions](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions)

  + [length](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions/length)?: number
  + [offset](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions/offset)?: number
  + [statCheck](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions/statCheck)?: (stats: [Stats](https://bun.com/reference/node/fs/Stats), headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders), statOptions: [StatOptions](https://bun.com/reference/node/http2/StatOptions)) => void
  + [waitForTrailers](https://bun.com/reference/node/http2/ServerStreamFileResponseOptions/waitForTrailers)?: boolean
* ### interface [ServerStreamFileResponseOptionsWithError](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError)

  + [length](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError/length)?: number
  + [offset](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError/offset)?: number
  + [onError](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError/onError)?: (err: ErrnoException) => void
  + [statCheck](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError/statCheck)?: (stats: [Stats](https://bun.com/reference/node/fs/Stats), headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders), statOptions: [StatOptions](https://bun.com/reference/node/http2/StatOptions)) => void
  + [waitForTrailers](https://bun.com/reference/node/http2/ServerStreamFileResponseOptionsWithError/waitForTrailers)?: boolean
* ### interface [ServerStreamResponseOptions](https://bun.com/reference/node/http2/ServerStreamResponseOptions)

  + [endStream](https://bun.com/reference/node/http2/ServerStreamResponseOptions/endStream)?: boolean
  + [waitForTrailers](https://bun.com/reference/node/http2/ServerStreamResponseOptions/waitForTrailers)?: boolean
* ### interface [SessionOptions](https://bun.com/reference/node/http2/SessionOptions)

  + [maxDeflateDynamicTableSize](https://bun.com/reference/node/http2/SessionOptions/maxDeflateDynamicTableSize)?: number

    Sets the maximum dynamic table size for deflating header fields.
  + [maxHeaderListPairs](https://bun.com/reference/node/http2/SessionOptions/maxHeaderListPairs)?: number

    Sets the maximum number of header entries. This is similar to `server.maxHeadersCount` or `request.maxHeadersCount` in the `node:http` module. The minimum value is `1`.
  + [maxOutstandingPings](https://bun.com/reference/node/http2/SessionOptions/maxOutstandingPings)?: number

    Sets the maximum number of outstanding, unacknowledged pings.
  + [maxSendHeaderBlockLength](https://bun.com/reference/node/http2/SessionOptions/maxSendHeaderBlockLength)?: number

    Sets the maximum allowed size for a serialized, compressed block of headers. Attempts to send headers that exceed this limit will result in a `'frameError'` event being emitted and the stream being closed and destroyed.
  + [maxSessionMemory](https://bun.com/reference/node/http2/SessionOptions/maxSessionMemory)?: number

    Sets the maximum memory that the `Http2Session` is permitted to use. The value is expressed in terms of number of megabytes, e.g. `1` equal 1 megabyte. The minimum value allowed is `1`. This is a credit based limit, existing `Http2Stream`s may cause this limit to be exceeded, but new `Http2Stream` instances will be rejected while this limit is exceeded. The current number of `Http2Stream` sessions, the current memory use of the header compression tables, current data queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all counted towards the current limit.
  + [maxSettings](https://bun.com/reference/node/http2/SessionOptions/maxSettings)?: number

    Sets the maximum number of settings entries per `SETTINGS` frame. The minimum value allowed is `1`.
  + [paddingStrategy](https://bun.com/reference/node/http2/SessionOptions/paddingStrategy)?: number

    Strategy used for determining the amount of padding to use for `HEADERS` and `DATA` frames.
  + [peerMaxConcurrentStreams](https://bun.com/reference/node/http2/SessionOptions/peerMaxConcurrentStreams)?: number

    Sets the maximum number of concurrent streams for the remote peer as if a `SETTINGS` frame had been received. Will be overridden if the remote peer sets its own value for `maxConcurrentStreams`.
  + [remoteCustomSettings](https://bun.com/reference/node/http2/SessionOptions/remoteCustomSettings)?: number[]

    The array of integer values determines the settings types, which are included in the `CustomSettings`-property of the received remoteSettings. Please see the `CustomSettings`-property of the `Http2Settings` object for more information, on the allowed setting types.
  + [settings](https://bun.com/reference/node/http2/SessionOptions/settings)?: [Settings](https://bun.com/reference/node/http2/Settings)

    The initial settings to send to the remote peer upon connection.
  + [strictFieldWhitespaceValidation](https://bun.com/reference/node/http2/SessionOptions/strictFieldWhitespaceValidation)?: boolean

    If `true`, it turns on strict leading and trailing whitespace validation for HTTP/2 header field names and values as per [RFC-9113](https://www.rfc-editor.org/rfc/rfc9113.html#section-8.2.1).
* ### interface [SessionState](https://bun.com/reference/node/http2/SessionState)

  + [deflateDynamicTableSize](https://bun.com/reference/node/http2/SessionState/deflateDynamicTableSize)?: number
  + [effectiveLocalWindowSize](https://bun.com/reference/node/http2/SessionState/effectiveLocalWindowSize)?: number
  + [effectiveRecvDataLength](https://bun.com/reference/node/http2/SessionState/effectiveRecvDataLength)?: number
  + [inflateDynamicTableSize](https://bun.com/reference/node/http2/SessionState/inflateDynamicTableSize)?: number
  + [lastProcStreamID](https://bun.com/reference/node/http2/SessionState/lastProcStreamID)?: number
  + [localWindowSize](https://bun.com/reference/node/http2/SessionState/localWindowSize)?: number
  + [nextStreamID](https://bun.com/reference/node/http2/SessionState/nextStreamID)?: number
  + [outboundQueueSize](https://bun.com/reference/node/http2/SessionState/outboundQueueSize)?: number
  + [remoteWindowSize](https://bun.com/reference/node/http2/SessionState/remoteWindowSize)?: number
* ### interface [Settings](https://bun.com/reference/node/http2/Settings)

  + [enablePush](https://bun.com/reference/node/http2/Settings/enablePush)?: boolean
  + [headerTableSize](https://bun.com/reference/node/http2/Settings/headerTableSize)?: number
  + [initialWindowSize](https://bun.com/reference/node/http2/Settings/initialWindowSize)?: number
  + [maxConcurrentStreams](https://bun.com/reference/node/http2/Settings/maxConcurrentStreams)?: number
  + [maxFrameSize](https://bun.com/reference/node/http2/Settings/maxFrameSize)?: number
  + [maxHeaderListSize](https://bun.com/reference/node/http2/Settings/maxHeaderListSize)?: number
* ### interface [StatOptions](https://bun.com/reference/node/http2/StatOptions)

  + [length](https://bun.com/reference/node/http2/StatOptions/length): number
  + [offset](https://bun.com/reference/node/http2/StatOptions/offset): number
* ### interface [StreamState](https://bun.com/reference/node/http2/StreamState)

  + [localClose](https://bun.com/reference/node/http2/StreamState/localClose)?: number
  + [localWindowSize](https://bun.com/reference/node/http2/StreamState/localWindowSize)?: number
  + [remoteClose](https://bun.com/reference/node/http2/StreamState/remoteClose)?: number
  + [state](https://bun.com/reference/node/http2/StreamState/state)?: number