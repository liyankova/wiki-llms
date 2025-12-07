---
url: https://bun.com/docs/guides/runtime/heap-snapshot
title: Inspect memory usage using V8 heap snapshots - Bun
source_domain: bun.com
---

# Inspect memory usage using V8 heap snapshots - Bun

Bun implements V8’s heap snapshot API, which allows you to create snapshots of the heap at runtime. This helps debug memory leaks in your JavaScript/TypeScript application.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)snapshot.ts

Copy

```
import v8 from "node:v8";

// Creates a heap snapshot file with an auto-generated name
const snapshotPath = v8.writeHeapSnapshot();
console.log(`Heap snapshot written to: ${snapshotPath}`);
```

---

## [​](https://bun.com/docs/guides/runtime/heap-snapshot#inspect-memory-in-chrome-devtools) Inspect memory in Chrome DevTools

To view V8 heap snapshots in Chrome DevTools:

1. Open Chrome DevTools (F12 or right-click and select “Inspect”)
2. Go to the “Memory” tab
3. Click the “Load” button (folder icon)
4. Select your `.heapsnapshot` file

![Chrome DevTools Memory Tab](https://mintcdn.com/bun-1dd33a4e/o4ey1PfJcT885lrd/images/chrome-devtools-memory.png?fit=max&auto=format&n=o4ey1PfJcT885lrd&q=85&s=8f11aeea8ad1f70974bb963f83c4decf)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/heap-snapshot.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/heap-snapshot)

⌘I