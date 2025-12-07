---
url: https://bun.com/docs/guides/runtime/timezone
title: Set a time zone in Bun - Bun
source_domain: bun.com
---

# Set a time zone in Bun - Bun

Bun supports programmatically setting a default time zone for the lifetime of the `bun` process. To do set, set the value of the `TZ` environment variable to a [valid timezone identifier](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

When running a file with `bun`, the timezone defaults to your system’s configured local time zone.When running tests with `bun test`, the timezone is set to `UTC` to make tests more deterministic.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)process.ts

Copy

```
process.env.TZ = "America/New_York";
```

---

Alternatively, this can be set from the command line when running a Bun command.

terminal

Copy

```
TZ=America/New_York bun run dev
```

---

Once `TZ` is set, any `Date` instances will have that time zone. By default all dates use your system’s configured time zone.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)process.ts

Copy

```
new Date().getHours(); // => 18

process.env.TZ = "America/New_York";

new Date().getHours(); // => 21
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/timezone.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/timezone)

⌘I