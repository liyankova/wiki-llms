---
url: https://bun.com/docs/runtime/file-system-router
title: File System Router - Bun
source_domain: bun.com
---

# File System Router - Bun

This API is primarily intended for library authors. At the moment only Next.js-style file-system routing is supported, but other styles may be added in the future.

## [​](https://bun.com/docs/runtime/file-system-router#next-js-style) Next.js-style

The `FileSystemRouter` class can resolve routes against a `pages` directory. (The Next.js 13 `app` directory is not yet supported.) Consider the following `pages` directory:

Copy

```
pages
├── index.tsx
├── settings.tsx
├── blog
│   ├── [slug].tsx
│   └── index.tsx
└── [[...catchall]].tsx
```

The `FileSystemRouter` can be used to resolve routes against this directory:

router.ts

Copy

```
const router = new Bun.FileSystemRouter({
  style: "nextjs",
  dir: "./pages",
  origin: "https://mydomain.com",
  assetPrefix: "_next/static/"
});

router.match("/");

// =>
{
  filePath: "/path/to/pages/index.tsx",
  kind: "exact",
  name: "/",
  pathname: "/",
  src: "https://mydomain.com/_next/static/pages/index.tsx"
}
```

Query parameters will be parsed and returned in the `query` property.

Copy

```
router.match("/settings?foo=bar");

// =>
{
  filePath: "/Users/colinmcd94/Documents/bun/fun/pages/settings.tsx",
  kind: "dynamic",
  name: "/settings",
  pathname: "/settings?foo=bar",
  src: "https://mydomain.com/_next/static/pages/settings.tsx",
  query: {
    foo: "bar"
  }
}
```

The router will automatically parse URL parameters and return them in the `params` property:

Copy

```
router.match("/blog/my-cool-post");

// =>
{
  filePath: "/Users/colinmcd94/Documents/bun/fun/pages/blog/[slug].tsx",
  kind: "dynamic",
  name: "/blog/[slug]",
  pathname: "/blog/my-cool-post",
  src: "https://mydomain.com/_next/static/pages/blog/[slug].tsx",
  params: {
    slug: "my-cool-post"
  }
}
```

The `.match()` method also accepts `Request` and `Response` objects. The `url` property will be used to resolve the route.

Copy

```
router.match(new Request("https://example.com/blog/my-cool-post"));
```

The router will read the directory contents on initialization. To re-scan the files, use the `.reload()` method.

Copy

```
router.reload();
```

## [​](https://bun.com/docs/runtime/file-system-router#reference) Reference

Copy

```
interface Bun {
  class FileSystemRouter {
    constructor(params: {
      dir: string;
      style: "nextjs";
      origin?: string;
      assetPrefix?: string;
      fileExtensions?: string[];
    });

    reload(): void;

    match(path: string | Request | Response): {
      filePath: string;
      kind: "exact" | "catch-all" | "optional-catch-all" | "dynamic";
      name: string;
      pathname: string;
      src: string;
      params?: Record<string, string>;
      query?: Record<string, string>;
    } | null
  }
}
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/file-system-router.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/file-system-router)

⌘I