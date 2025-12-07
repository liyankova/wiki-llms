---
url: https://bun.com/docs/guides/http/file-uploads
title: Upload files via HTTP using FormData - Bun
source_domain: bun.com
---

# Upload files via HTTP using FormData - Bun

To upload files via HTTP with Bun, use the [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) API. Let’s start with a HTTP server that serves a simple HTML web form.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const server = Bun.serve({
  port: 4000,
  async fetch(req) {
    const url = new URL(req.url);

    // return index.html for root path
    if (url.pathname === "/")
      return new Response(Bun.file("index.html"), {
        headers: {
          "Content-Type": "text/html",
        },
      });

    return new Response("Not Found", { status: 404 });
  },
});

console.log(`Listening on http://localhost:${server.port}`);
```

---

We can define our HTML form in another file, `index.html`.

index.html

Copy

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Form</title>
  </head>
  <body>
    <form action="/action" method="post" enctype="multipart/form-data">
      <input type="text" name="name" placeholder="Name" />
      <input type="file" name="profilePicture" />
      <input type="submit" value="Submit" />
    </form>
  </body>
</html>
```

---

At this point, we can run the server and visit [`localhost:4000`](http://localhost:4000) to see our form.

Copy

```
bun run index.ts
Listening on http://localhost:4000
```

---

Our form will send a `POST` request to the `/action` endpoint with the form data. Let’s handle that request in our server.
First we use the [`.formData()`](https://developer.mozilla.org/en-US/docs/Web/API/Request/formData) method on the incoming `Request` to asynchronously parse its contents to a `FormData` instance. Then we can use the [`.get()`](https://developer.mozilla.org/en-US/docs/Web/API/FormData/get) method to extract the value of the `name` and `profilePicture` fields. Here `name` corresponds to a `string` and `profilePicture` is a `Blob`.
Finally, we write the `Blob` to disk using [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write).

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const server = Bun.serve({
  port: 4000,
  async fetch(req) {
    const url = new URL(req.url);

    // return index.html for root path
    if (url.pathname === "/")
      return new Response(Bun.file("index.html"), {
        headers: {
          "Content-Type": "text/html",
        },
      });

    // parse formdata at /action
    if (url.pathname === "/action") { 
      const formdata = await req.formData(); 
      const name = formdata.get("name"); 
      const profilePicture = formdata.get("profilePicture"); 
      if (!profilePicture) throw new Error("Must upload a profile picture."); 
      // write profilePicture to disk
      await Bun.write("profilePicture.png", profilePicture); 
      return new Response("Success"); 
    } 

    return new Response("Not Found", { status: 404 });
  },
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/file-uploads.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/file-uploads)

⌘I