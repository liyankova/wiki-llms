---
url: https://bun.com/blog/bun-v1.0.3
title: Bun v1.0.3 | Bun Blog
source_domain: bun.com
---

# Bun v1.0.3 | Bun Blog

# Bun v1.0.3

---

[Colin McDonnell](https://twitter.com/colinhacks) · September 22, 2023

Bun v1.0.3 fixes numerous bugs, adds support for metadata reflection via TypeScript's [`emitDecoratorMetadata`](https://www.typescriptlang.org/tsconfig#emitDecoratorMetadata), improves `fetch` compatibility, unblocks private registries like Azure Artifacts and Artifactory, bunx bugfix, console.log() depth 8 -> 2, Node.js compatibility improvements, and more.

Thank you for reporting issues. We are working hard to fix them as quickly as possible.

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one. We've been releasing a lot of changes to Bun recently. Here's a recap of the last few releases. In case you missed it:

* [`v1.0.0`](https://bun.com/blog/bun-v1.0) - Bun's first stable release!
* [`v1.0.1`](https://bun.com/blog/bun-v1.0.1) - Named imports for .json & .toml files, bugfixes to bun install, node:path, Buffer
* [`v1.0.2`](https://bun.com/blog/bun-v1.0.2) - Make `--watch` faster, plus bug fixes

To install Bun:

curl

npm

brew

docker

curl

```
curl -fsSL https://bun.sh/install | bash
```

npm

```
npm install -g bun
```

brew

```
brew tap oven-sh/bun
```

```
brew install bun
```

docker

```
docker pull oven/bun
```

```
docker run --rm --init --ulimit memlock=-1:-1 oven/bun
```

To upgrade Bun:

```
bun upgrade
```

## [`emitDecoratorMetadata` (used by Nest.js, TypeORM, and more)](https://bun.com/blog/bun-v1.0.3#emitdecoratormetadata-used-by-nest-js-typeorm-and-more)

Bun now supports metadata reflection via TypeScript's [`emitDecoratorMetadata`](https://www.typescriptlang.org/tsconfig#emitDecoratorMetadata). This means that you can use Nest.js with Bun, and it will work out of the box.

tsconfig.json

```
{
  "compilerOptions": {
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true
  }
}
```

The `emitDecoratorMetadata` is a TypeScript compiler option that enables the generation of metadata for decorators via [reflect-metadata](https://www.npmjs.com/package/reflect-metadata).

## [Improved Nest.js support](https://bun.com/blog/bun-v1.0.3#improved-nest-js-support)

The addition of `emitDecoratorMetadata` dramatically improves Nest.js support, as it relies on custom ["Reflectors"](https://docs.nestjs.com/fundamentals/execution-context#reflection-and-metadata) to attach metadata and middleware to route handlers.

```
@Post()
@Roles(['admin']) // custom authentication decorator
async create(@Body() createCatDto: CreateCatDto) {
  this.catsService.create(createCatDto);
}
```

## [`module.parent` support](https://bun.com/blog/bun-v1.0.3#module-parent-support)

In Node, the CommonJS `module.parent` getter is a reference to the parent module that required the current module. This is useful for determining whether a module was run directly or required by another module.

```
if (module.parent) {
  // this module was required by another module
} else {
  // this module was run directly
}
```

Bun now supports `module.parent` in the same way that Node does.

For ES modules, you can use `import.meta.main` to find out if the current module started the Bun process.

## [Bugfixes for private npm registries](https://bun.com/blog/bun-v1.0.3#bugfixes-for-private-npm-registries)

Improvements to [`fetch`](https://github.com/oven-sh/bun/pull/5729) unblock the usage of `bun install` with popular private package registries like Azure Artifacts and JFrog Artifactory.

You can configure a private registry using `bunfig.toml` instead of `.npmrc`. Provide values for `url`, `username`, and `password` under the `[install.registry]` section of your `bunfig.toml` file.

bunfig.toml

```
[install.registry]
url = "https://pkgs.dev.azure.com/my-azure-artifacts-user/_packaging/my-azure-artifacts-user/npm/registry"
username = "my-azure-artifacts-user"
# Bun v1.0.3+ supports using an environment variable here
password = "$NPM_PASSWORD"
```

Alternatively, specify a token instead of a username and password. This is useful for Artifactory.

bunfig.toml

```
[install.registry]
url = "https://my-artifactory-server.com/artifactory/api/npm/npm-virtual"
token = "$NPM_TOKEN"
```

For more complete information, refer to our new guides:

* [Using `bun install` with Artifactory](https://bun.com/guides/install/jfrog-artifactory)
* [Using `bun install` with Azure Artifacts](https://bun.com/guides/install/azure-artifacts)

## [`[0.5ms] env` message is now silent by default](https://bun.com/blog/bun-v1.0.3#0-5ms-env-message-is-now-silent-by-default)

Many people asked for this, so @colinhacks made it happen. The `[0.5ms] env loaded` message is now silent by default. You can still see it by setting `logLevel` to `"debug"` in `bunfig.toml`

> in the next version of bun  
>   
> [0.1ms] ".env" is silenced by default [pic.twitter.com/F7V6hGZvrV](https://t.co/F7V6hGZvrV)
>
> — Jarred Sumner (@jarredsumner) [September 22, 2023](https://twitter.com/jarredsumner/status/1705102614793474448?ref_src=twsrc%5Etfw)

## [Node.js compatiblity improvements](https://bun.com/blog/bun-v1.0.3#node-js-compatiblity-improvements)

The work on Node.js compatibility continues. Here are some of the improvements in this release:

### [Implement `console.Console` constructor](https://bun.com/blog/bun-v1.0.3#implement-console-console-constructor)

The Node.js `console.Console` constructor has been implemented.

```
import { Console } from "console";
import { createWriteStream } from "fs";

const writer = new Console({ stdout: createWriteStream("log.txt") });

writer.log("hello");
writer.log("world", { x: 2 });
```

This fixes [`vitest`](https://github.com/oven-sh/bun/issues/4145) and webpack's [`ts-loader`](https://github.com/oven-sh/bun/issues/5558) when executed with the Bun runtime—though consider using `bun test` and `bun build` instead! Of course, there are a lot of tools and codebases that rely on these technologies which will now work with Bun.

#### Empty environment variables now appear as an empty string (`""`)

In `process.env` and `Bun.env`, empty environment variables appeared as `undefined` instead of an empty string. This is fixed, thanks to [@liz3](https://github.com/liz3).

#### `dns.lookupService` is now implemented

The `node:dns` function `dns.lookupService` is now implemented. Thanks to [@Hanaasagi](https://github.com/Hanaasagi).

#### console.log() depth is now 2 instead of 8

8 was nice, but caused issues with large objects filling up your terminal screen. Thanks to [@JibranKalia](https://github.com/JibranKalia). This aligns the behavior with Node.js.

#### node\_api\_create\_external\_string\_latin1 and node\_api\_create\_external\_string\_utf16

The node\_api functions `node_api_create_external_string_latin1` and `node_api_create_external_string_utf16` are now implemented

#### listen() in `node:http` callback bugfix

The error event was not emitting to the event listener correctly. Thanks to [@SuperAuguste](https://github.com/SuperAuguste) for fixing this.

## [Bugfixes](https://bun.com/blog/bun-v1.0.3#bugfixes)

#### Crash in `request.json()` fixed

A crash that could occur when calling `request.json()` was fixed. It was caused by incorrect exception handling in native code.

#### `bun pm rm cache` now works

The `bun pm rm cache` command now deletes the cache directory. Thanks to [@WingLim](https://github.com/WingLim).

#### Max redirect URL length is now 8192 instead of 4096

This fixes an issue with certain private npm registries.

#### bunx choosing version from $PATH instead of @version tag bugfix

A bug causing `bunx` to choose the version of the executable from `$PATH` instead of the `@version` tag was fixed

> in the next version of bun  
>   
> bunx foo@tag will always load the @tag version when a @tag is present, instead of choosing the version in [$PATH](https://twitter.com/search?q=%24PATH&src=ctag&ref_src=twsrc%5Etfw) [pic.twitter.com/eCMVa0gSxF](https://t.co/eCMVa0gSxF)
>
> — Jarred Sumner (@jarredsumner) [September 20, 2023](https://twitter.com/jarredsumner/status/1704390982534594744?ref_src=twsrc%5Etfw)

## [Full changelog](https://bun.com/blog/bun-v1.0.3#full-changelog)

| [`#4652`](https://github.com/oven-sh/bun/pull/4652) | VSCode Extension Bunlock Syntax-Highlighting and Docs Improvements by [@JeremyFunk](https://bun.com/blog/JeremyFunk) |
| [`#5451`](https://github.com/oven-sh/bun/pull/5451) | docs(runtime): fix some typo. by [@zongzi531](https://bun.com/blog/zongzi531) |
| [`#5531`](https://github.com/oven-sh/bun/pull/5531) | Update development.md by [@sonyarianto](https://bun.com/blog/sonyarianto) |
| [`#5525`](https://github.com/oven-sh/bun/pull/5525) | fix(corking) uncork if needed by [@cirospaciari](https://bun.com/blog/cirospaciari) |
| [`#5503`](https://github.com/oven-sh/bun/pull/5503) | fix(request) handle undefined/null/empty signal on request by [@cirospaciari](https://bun.com/blog/cirospaciari) |
| [`#5521`](https://github.com/oven-sh/bun/pull/5521) | fix(bundler): Add a space before minified require by [@davidmhewitt](https://bun.com/blog/davidmhewitt) |
| [`#5505`](https://github.com/oven-sh/bun/pull/5505) | fix(node/fs.watch): Check first char before trimming event filenames by [@davidmhewitt](https://bun.com/blog/davidmhewitt) |
| [`#5535`](https://github.com/oven-sh/bun/pull/5535) | webkit upgrade by [@dylan-conway](https://bun.com/blog/dylan-conway) |
| [`#5555`](https://github.com/oven-sh/bun/pull/5555) | Follow-up for workspace docs #5379 and #5229 by [@bdenham](https://bun.com/blog/bdenham) |
| [`#5579`](https://github.com/oven-sh/bun/pull/5579) | fix: `ArrayBufferConstructor` type signature by [@52](https://bun.com/blog/52) |
| [`#5580`](https://github.com/oven-sh/bun/pull/5580) | fix: `array-buffer.test-d.ts` test by [@52](https://bun.com/blog/52) |
| [`#4693`](https://github.com/oven-sh/bun/pull/4693) | fix: node compatibility with empty path string (stat, exist, ...) by [@coratgerl](https://bun.com/blog/coratgerl) |
| [`#5603`](https://github.com/oven-sh/bun/pull/5603) | Make error message when importing a node: module in a browser bundle clearer by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5576`](https://github.com/oven-sh/bun/pull/5576) | docs: fix typo in lockflie nav by [@Vilsol](https://bun.com/blog/Vilsol) |
| [`#5593`](https://github.com/oven-sh/bun/pull/5593) | Docs: path aliases fix by [@e253](https://bun.com/blog/e253) |
| [`#5496`](https://github.com/oven-sh/bun/pull/5496) | fix(fetch) handle 100 continue by [@cirospaciari](https://bun.com/blog/cirospaciari) |
| [`#5387`](https://github.com/oven-sh/bun/pull/5387) | feat(encoding): TextDecoder support undefined by [@WingLim](https://bun.com/blog/WingLim) |
| [`#5481`](https://github.com/oven-sh/bun/pull/5481) | fix(child\_process) unref next tick so exit/close event can be fired before application exits by [@cirospaciari](https://bun.com/blog/cirospaciari) |
| [`#5529`](https://github.com/oven-sh/bun/pull/5529) | Implement VSCode tasks for bun by [@JeremyFunk](https://bun.com/blog/JeremyFunk) |
| [`#5610`](https://github.com/oven-sh/bun/pull/5610) | fix(install): Return NotSupported when errno == XDEV by [@pan93412](https://bun.com/blog/pan93412) |
| [`#5510`](https://github.com/oven-sh/bun/pull/5510) | Fix ZLS commit hash in the document by [@shinichy](https://bun.com/blog/shinichy) |
| [`#5628`](https://github.com/oven-sh/bun/pull/5628) | Added .DS\_Store to gitignore-for-init by [@Cilooth](https://bun.com/blog/Cilooth) |
| [`#5615`](https://github.com/oven-sh/bun/pull/5615) | Workaround #5604 by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5626`](https://github.com/oven-sh/bun/pull/5626) | Fix a TypeError in the documentation by [@LapsTimeOFF](https://bun.com/blog/LapsTimeOFF) |
| [`#5656`](https://github.com/oven-sh/bun/pull/5656) | Add a way to disable the GC timer by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5660`](https://github.com/oven-sh/bun/pull/5660) | Remove hardcoded references to zig in Makefile by [@xbjfk](https://bun.com/blog/xbjfk) |
| [`#5595`](https://github.com/oven-sh/bun/pull/5595) | feat(console.log): Print anonymous when class name is unknown by [@JibranKalia](https://bun.com/blog/JibranKalia) |
| [`#5572`](https://github.com/oven-sh/bun/pull/5572) | feat(test): Implement `arrayContaining` by [@WingLim](https://bun.com/blog/WingLim) |
| [`#5655`](https://github.com/oven-sh/bun/pull/5655) | In `bun:sqlite`, make sure we set the number tag correctly when creating the JSValue by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5662`](https://github.com/oven-sh/bun/pull/5662) | fix(config): support for registry url without trailing slash by [@Hanaasagi](https://bun.com/blog/Hanaasagi) |
| [`#5685`](https://github.com/oven-sh/bun/pull/5685) | fix(docs): update formatting by [@rauny-brandao](https://bun.com/blog/rauny-brandao) |
| [`#5638`](https://github.com/oven-sh/bun/pull/5638) | docs: add missing options from bun init by [@jumoog](https://bun.com/blog/jumoog) |
| [`#5594`](https://github.com/oven-sh/bun/pull/5594) | change circles for color-blinds by [@Hamcker](https://bun.com/blog/Hamcker) |
| [`#5689`](https://github.com/oven-sh/bun/pull/5689) | Fix HTTP listen behavior being non-compliant with node by [@paperclover](https://bun.com/blog/paperclover) |
| [`#5448`](https://github.com/oven-sh/bun/pull/5448) | feat(runtime): Implement `console.Console` by [@paperclover](https://bun.com/blog/paperclover) |
| [`#5675`](https://github.com/oven-sh/bun/pull/5675) | Implement `node_api_create_external_string_latin1` by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5699`](https://github.com/oven-sh/bun/pull/5699) | fix(runtime/node): Allow `new Buffer.alloc()` + Upgrade WebKit by [@paperclover](https://bun.com/blog/paperclover) |
| [`#5684`](https://github.com/oven-sh/bun/pull/5684) | fix: remove unneeded branch in toJSONWithBytes by [@liz3](https://bun.com/blog/liz3) |
| [`#5696`](https://github.com/oven-sh/bun/pull/5696) | update llvm version from 15 to 16 in makefile by [@nithinkjoy-tech](https://bun.com/blog/nithinkjoy-tech) |
| [`#5679`](https://github.com/oven-sh/bun/pull/5679) | fix: provide empty string to 0 length process environment variables by [@liz3](https://bun.com/blog/liz3) |
| [`#5025`](https://github.com/oven-sh/bun/pull/5025) | `bun run` fix missing script error on empty file by [@Parzival-3141](https://bun.com/blog/Parzival-3141) |
| [`#5444`](https://github.com/oven-sh/bun/pull/5444) | Add navigator type definition by [@ruihe774](https://bun.com/blog/ruihe774) |
| [`#5716`](https://github.com/oven-sh/bun/pull/5716) | Encode slashes in package names in the registry manifest request by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5726`](https://github.com/oven-sh/bun/pull/5726) | Make bun install --verbose more verbose by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5730`](https://github.com/oven-sh/bun/pull/5730) | Fixes #3712 by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5729`](https://github.com/oven-sh/bun/pull/5729) | Align fetch() redirect behavior with spec by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5744`](https://github.com/oven-sh/bun/pull/5744) | Get artifactory to work by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5702`](https://github.com/oven-sh/bun/pull/5702) | docs: Update Remix guide by [@brookslybrand](https://bun.com/blog/brookslybrand) |
| [`#5620`](https://github.com/oven-sh/bun/pull/5620) | Added react installation to react.md by [@jt3k](https://bun.com/blog/jt3k) |
| [`#5597`](https://github.com/oven-sh/bun/pull/5597) | remind users of the latest version by [@jumoog](https://bun.com/blog/jumoog) |
| [`#5562`](https://github.com/oven-sh/bun/pull/5562) | docs: update `net` node documentation by [@weyert](https://bun.com/blog/weyert) |
| [`#5513`](https://github.com/oven-sh/bun/pull/5513) | docs(development): typo which would lead to wrong llvm installation by [@sum117](https://bun.com/blog/sum117) |
| [`#5759`](https://github.com/oven-sh/bun/pull/5759) | Doc updates by [@colinhacks](https://bun.com/blog/colinhacks) |
| [`#4571`](https://github.com/oven-sh/bun/pull/4571) | fix(cli): `bun pm cache rm` command not work by [@WingLim](https://bun.com/blog/WingLim) |
| [`#5762`](https://github.com/oven-sh/bun/pull/5762) | fix(Makefile) by [@cirospaciari](https://bun.com/blog/cirospaciari) |
| [`#5775`](https://github.com/oven-sh/bun/pull/5775) | Fixes #5769 by [@Jarred-Sumner](https://bun.com/blog/Jarred-Sumner) |
| [`#5447`](https://github.com/oven-sh/bun/pull/5447) | add warning to Ensure correct placement of the '--watch' flag by [@a4addel](https://bun.com/blog/a4addel) |
| [`#5456`](https://github.com/oven-sh/bun/pull/5456) | Updated modules.md to address issue #5420 by [@h2210316651](https://bun.com/blog/h2210316651) |
| [`#4810`](https://github.com/oven-sh/bun/pull/4810) | docs: add Qwik guide by [@sanyamkamat](https://bun.com/blog/sanyamkamat) |

## [New contributors](https://bun.com/blog/bun-v1.0.3#new-contributors)

Thanks to Bun's newest contributors!

* @52 made their first contribution in https://github.com/oven-sh/bun/pull/5579
* @a4addel made their first contribution in https://github.com/oven-sh/bun/pull/5447
* @AaronDewes made their first contribution in https://github.com/oven-sh/bun/pull/4779
* @bdenham made their first contribution in https://github.com/oven-sh/bun/pull/5555
* @brookslybrand made their first contribution in https://github.com/oven-sh/bun/pull/5702
* @Brooooooklyn made their first contribution in https://github.com/oven-sh/bun/pull/5788
* @Cilooth made their first contribution in https://github.com/oven-sh/bun/pull/5628
* @coratgerl made their first contribution in https://github.com/oven-sh/bun/pull/4693
* @ggobbe made their first contribution in https://github.com/oven-sh/bun/pull/5786
* @h2210316651 made their first contribution in https://github.com/oven-sh/bun/pull/5456
* @Hamcker made their first contribution in https://github.com/oven-sh/bun/pull/5594
* @igorshapiro made their first contribution in https://github.com/oven-sh/bun/pull/5873
* @ImBIOS made their first contribution in https://github.com/oven-sh/bun/pull/5885
* @JeremyFunk made their first contribution in https://github.com/oven-sh/bun/pull/4652
* @JibranKalia made their first contribution in https://github.com/oven-sh/bun/pull/5595
* @jonahsnider made their first contribution in https://github.com/oven-sh/bun/pull/5104
* @jt3k made their first contribution in https://github.com/oven-sh/bun/pull/5620
* @jumoog made their first contribution in https://github.com/oven-sh/bun/pull/5638
* @liz3 made their first contribution in https://github.com/oven-sh/bun/pull/5684
* @nithinkjoy-tech made their first contribution in https://github.com/oven-sh/bun/pull/5696
* @pan93412 made their first contribution in https://github.com/oven-sh/bun/pull/5610
* @rauny-brandao made their first contribution in https://github.com/oven-sh/bun/pull/5685
* @ruihe774 made their first contribution in https://github.com/oven-sh/bun/pull/5444
* @sanyamkamat made their first contribution in https://github.com/oven-sh/bun/pull/4810
* @shinichy made their first contribution in https://github.com/oven-sh/bun/pull/5510
* @sum117 made their first contribution in https://github.com/oven-sh/bun/pull/5513
* @Vilsol made their first contribution in https://github.com/oven-sh/bun/pull/5576
* @weyert made their first contribution in https://github.com/oven-sh/bun/pull/5562
* @xbjfk made their first contribution in https://github.com/oven-sh/bun/pull/5660
* @yadav-saurabh made their first contribution in https://github.com/oven-sh/bun/pull/5270

---

[#### Bun v1.0.2](https://bun.com/blog/bun-v1.0.2)[#### Bun v1.0.4](https://bun.com/blog/bun-v1.0.4)