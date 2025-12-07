---
url: https://bun.com/reference/node/module
title: Node.js module module | API Reference | Bun
source_domain: bun.com
---

# Node.js module module | API Reference | Bun

Node.js module

# [module](https://bun.com/reference/node/module)

The `'node:module'` module provides utilities for interacting with Node.js's module loading system. You can create custom `Module equire` functions, inspect module cache, and evaluate code in isolated contexts.

Works in Bun

Core CJS (require) and ESM (import) functionality works. Overriding require.cache is supported. However, `module.register` (for loaders) is not implemented (use Bun plugins). Some Module methods and internal properties (`\_extensions`, `\_pathCache`, `\_cache`) are missing or no-ops.

* ### [export default namespace module](https://bun.com/reference/node/module/default)

  + ### namespace [constants](https://bun.com/reference/node/module/default/constants)

    - ### namespace [compileCacheStatus](https://bun.com/reference/node/module/default/constants/compileCacheStatus)

      The following constants are returned as the `status` field in the object returned by enableCompileCache to indicate the result of the attempt to enable the [module compile cache](https://nodejs.org/docs/latest-v24.x/api/module.html#module-compile-cache).

      * const [ALREADY\_ENABLED](https://bun.com/reference/node/module/default/constants/compileCacheStatus/ALREADY_ENABLED): number

        The compile cache has already been enabled before, either by a previous call to enableCompileCache, or by the `NODE_COMPILE_CACHE=dir` environment variable. The directory used to store the compile cache will be returned in the `directory` field in the returned object.
      * const [DISABLED](https://bun.com/reference/node/module/default/constants/compileCacheStatus/DISABLED): number

        Node.js cannot enable the compile cache because the environment variable `NODE_DISABLE_COMPILE_CACHE=1` has been set.
      * const [ENABLED](https://bun.com/reference/node/module/default/constants/compileCacheStatus/ENABLED): number

        Node.js has enabled the compile cache successfully. The directory used to store the compile cache will be returned in the `directory` field in the returned object.
      * const [FAILED](https://bun.com/reference/node/module/default/constants/compileCacheStatus/FAILED): number

        Node.js fails to enable the compile cache. This can be caused by the lack of permission to use the specified directory, or various kinds of file system errors. The detail of the failure will be returned in the `message` field in the returned object.
  + ### class [SourceMap](https://bun.com/reference/node/module/default/SourceMap)

    - readonly [payload](https://bun.com/reference/node/module/default/SourceMap/payload): [SourceMapPayload](https://bun.com/reference/node/module/default/SourceMapPayload)

      Getter for the payload used to construct the `SourceMap` instance.
    - [findEntry](https://bun.com/reference/node/module/default/SourceMap/findEntry)(

      lineOffset: number,

      columnOffset: number

      ): {} | [SourceMapping](https://bun.com/reference/node/module/default/SourceMapping);

      Given a line offset and column offset in the generated source file, returns an object representing the SourceMap range in the original file if found, or an empty object if not.

      The object returned contains the following keys:

      The returned value represents the raw range as it appears in the SourceMap, based on zero-indexed offsets, *not* 1-indexed line and column numbers as they appear in Error messages and CallSite objects.

      To get the corresponding 1-indexed line and column numbers from a lineNumber and columnNumber as they are reported by Error stacks and CallSite objects, use `sourceMap.findOrigin(lineNumber, columnNumber)`

      @param lineOffset

      The zero-indexed line number offset in the generated source

      @param columnOffset

      The zero-indexed column number offset in the generated source
    - [findOrigin](https://bun.com/reference/node/module/default/SourceMap/findOrigin)(

      lineNumber: number,

      columnNumber: number

      ): {} | [SourceOrigin](https://bun.com/reference/node/module/default/SourceOrigin);

      Given a 1-indexed `lineNumber` and `columnNumber` from a call site in the generated source, find the corresponding call site location in the original source.

      If the `lineNumber` and `columnNumber` provided are not found in any source map, then an empty object is returned.

      @param lineNumber

      The 1-indexed line number of the call site in the generated source

      @param columnNumber

      The 1-indexed column number of the call site in the generated source
  + ### interface [EnableCompileCacheResult](https://bun.com/reference/node/module/default/EnableCompileCacheResult)

    - [directory](https://bun.com/reference/node/module/default/EnableCompileCacheResult/directory)?: string

      If the compile cache is enabled, this contains the directory where the compile cache is stored. Only set if `status` is `module.constants.compileCacheStatus.ENABLED` or `module.constants.compileCacheStatus.ALREADY_ENABLED`.
    - [message](https://bun.com/reference/node/module/default/EnableCompileCacheResult/message)?: string

      If Node.js cannot enable the compile cache, this contains the error message. Only set if `status` is `module.constants.compileCacheStatus.FAILED`.
    - [status](https://bun.com/reference/node/module/default/EnableCompileCacheResult/status): number

      One of the constants.compileCacheStatus
  + ### interface [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes)

    - [type](https://bun.com/reference/node/module/default/ImportAttributes/type)?: string
  + ### interface [LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput)

    - [format](https://bun.com/reference/node/module/default/LoadFnOutput/format): undefined | null | string
    - [shortCircuit](https://bun.com/reference/node/module/default/LoadFnOutput/shortCircuit)?: boolean

      A signal that this hook intends to terminate the chain of `resolve` hooks.
    - [source](https://bun.com/reference/node/module/default/LoadFnOutput/source)?: [ModuleSource](https://bun.com/reference/node/module/default/ModuleSource)

      The source for Node.js to evaluate
  + ### interface [LoadHookContext](https://bun.com/reference/node/module/default/LoadHookContext)

    - [conditions](https://bun.com/reference/node/module/default/LoadHookContext/conditions): string[]

      Export conditions of the relevant `package.json`
    - [format](https://bun.com/reference/node/module/default/LoadHookContext/format): undefined | null | string

      The format optionally supplied by the `resolve` hook chain (can be an intermediary value).
    - [importAttributes](https://bun.com/reference/node/module/default/LoadHookContext/importAttributes): [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes)

      An object whose key-value pairs represent the assertions for the module to import
  + ### interface [ModuleHooks](https://bun.com/reference/node/module/default/ModuleHooks)

    - [deregister](https://bun.com/reference/node/module/default/ModuleHooks/deregister)(): void;

      Deregister the hook instance.
  + ### interface [RegisterHooksOptions](https://bun.com/reference/node/module/default/RegisterHooksOptions)

    - [load](https://bun.com/reference/node/module/default/RegisterHooksOptions/load)?: [LoadHookSync](https://bun.com/reference/node/module/default/LoadHookSync)

      See [load hook](https://nodejs.org/docs/latest-v24.x/api/module.html#loadurl-context-nextload).
    - [resolve](https://bun.com/reference/node/module/default/RegisterHooksOptions/resolve)?: [ResolveHookSync](https://bun.com/reference/node/module/default/ResolveHookSync)

      See [resolve hook](https://nodejs.org/docs/latest-v24.x/api/module.html#resolvespecifier-context-nextresolve).
  + ### interface [RegisterOptions](https://bun.com/reference/node/module/default/RegisterOptions)<Data>

    - [data](https://bun.com/reference/node/module/default/RegisterOptions/data)?: Data

      Any arbitrary, cloneable JavaScript value to pass into the initialize hook.
    - [parentURL](https://bun.com/reference/node/module/default/RegisterOptions/parentURL)?: string | [URL](https://bun.com/reference/node/url/URL)

      If you want to resolve `specifier` relative to a base URL, such as `import.meta.url`, you can pass that URL here. This property is ignored if the `parentURL` is supplied as the second argument.
    - [transferList](https://bun.com/reference/node/module/default/RegisterOptions/transferList)?: any[]

      [Transferable objects](https://nodejs.org/docs/latest-v24.x/api/worker_threads.html#portpostmessagevalue-transferlist) to be passed into the `initialize` hook.
  + ### interface [ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput)

    - [format](https://bun.com/reference/node/module/default/ResolveFnOutput/format)?: null | string

      A hint to the load hook (it might be ignored); can be an intermediary value.
    - [importAttributes](https://bun.com/reference/node/module/default/ResolveFnOutput/importAttributes)?: [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes)

      The import attributes to use when caching the module (optional; if excluded the input will be used)
    - [shortCircuit](https://bun.com/reference/node/module/default/ResolveFnOutput/shortCircuit)?: boolean

      A signal that this hook intends to terminate the chain of `resolve` hooks.
    - [url](https://bun.com/reference/node/module/default/ResolveFnOutput/url): string

      The absolute URL to which this input resolves
  + ### interface [ResolveHookContext](https://bun.com/reference/node/module/default/ResolveHookContext)

    - [conditions](https://bun.com/reference/node/module/default/ResolveHookContext/conditions): string[]

      Export conditions of the relevant `package.json`
    - [importAttributes](https://bun.com/reference/node/module/default/ResolveHookContext/importAttributes): [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes)

      An object whose key-value pairs represent the assertions for the module to import
    - [parentURL](https://bun.com/reference/node/module/default/ResolveHookContext/parentURL): undefined | string

      The module importing this one, or undefined if this is the Node.js entry point
  + ### interface [SetSourceMapsSupportOptions](https://bun.com/reference/node/module/default/SetSourceMapsSupportOptions)

    - [generatedCode](https://bun.com/reference/node/module/default/SetSourceMapsSupportOptions/generatedCode)?: boolean

      If enabling the support for generated code from `eval` or `new Function`.
    - [nodeModules](https://bun.com/reference/node/module/default/SetSourceMapsSupportOptions/nodeModules)?: boolean

      If enabling the support for files in `node_modules`.
  + ### interface [SourceMapConstructorOptions](https://bun.com/reference/node/module/default/SourceMapConstructorOptions)

    - [lineLengths](https://bun.com/reference/node/module/default/SourceMapConstructorOptions/lineLengths)?: readonly number[]
  + ### interface [SourceMapPayload](https://bun.com/reference/node/module/default/SourceMapPayload)

    - [file](https://bun.com/reference/node/module/default/SourceMapPayload/file): string
    - [mappings](https://bun.com/reference/node/module/default/SourceMapPayload/mappings): string
    - [names](https://bun.com/reference/node/module/default/SourceMapPayload/names): string[]
    - [sourceRoot](https://bun.com/reference/node/module/default/SourceMapPayload/sourceRoot): string
    - [sources](https://bun.com/reference/node/module/default/SourceMapPayload/sources): string[]
    - [sourcesContent](https://bun.com/reference/node/module/default/SourceMapPayload/sourcesContent): string[]
    - [version](https://bun.com/reference/node/module/default/SourceMapPayload/version): number
  + ### interface [SourceMapping](https://bun.com/reference/node/module/default/SourceMapping)

    - [generatedColumn](https://bun.com/reference/node/module/default/SourceMapping/generatedColumn): number
    - [generatedLine](https://bun.com/reference/node/module/default/SourceMapping/generatedLine): number
    - [originalColumn](https://bun.com/reference/node/module/default/SourceMapping/originalColumn): number
    - [originalLine](https://bun.com/reference/node/module/default/SourceMapping/originalLine): number
    - [originalSource](https://bun.com/reference/node/module/default/SourceMapping/originalSource): string
  + ### interface [SourceMapsSupport](https://bun.com/reference/node/module/default/SourceMapsSupport)

    - [enabled](https://bun.com/reference/node/module/default/SourceMapsSupport/enabled): boolean

      If the source maps support is enabled
    - [generatedCode](https://bun.com/reference/node/module/default/SourceMapsSupport/generatedCode): boolean

      If the support is enabled for generated code from `eval` or `new Function`.
    - [nodeModules](https://bun.com/reference/node/module/default/SourceMapsSupport/nodeModules): boolean

      If the support is enabled for files in `node_modules`.
  + ### interface [SourceOrigin](https://bun.com/reference/node/module/default/SourceOrigin)

    - [columnNumber](https://bun.com/reference/node/module/default/SourceOrigin/columnNumber): number

      The 1-indexed columnNumber of the corresponding call site in the original source
    - [fileName](https://bun.com/reference/node/module/default/SourceOrigin/fileName): string

      The file name of the original source, as reported in the SourceMap
    - [lineNumber](https://bun.com/reference/node/module/default/SourceOrigin/lineNumber): number

      The 1-indexed lineNumber of the corresponding call site in the original source
    - [name](https://bun.com/reference/node/module/default/SourceOrigin/name): undefined | string

      The name of the range in the source map, if one was provided
  + ### interface [StripTypeScriptTypesOptions](https://bun.com/reference/node/module/default/StripTypeScriptTypesOptions)

    - [mode](https://bun.com/reference/node/module/default/StripTypeScriptTypesOptions/mode)?: 'strip' | 'transform'

      Possible values are:

      * `'strip'` Only strip type annotations without performing the transformation of TypeScript features.
      * `'transform'` Strip type annotations and transform TypeScript features to JavaScript.
    - [sourceMap](https://bun.com/reference/node/module/default/StripTypeScriptTypesOptions/sourceMap)?: boolean

      Only when `mode` is `'transform'`, if `true`, a source map will be generated for the transformed code.
    - [sourceUrl](https://bun.com/reference/node/module/default/StripTypeScriptTypesOptions/sourceUrl)?: string

      Specifies the source url used in the source map.
  + type [ImportPhase](https://bun.com/reference/node/module/default/ImportPhase) = 'source' | 'evaluation'
  + type [InitializeHook](https://bun.com/reference/node/module/default/InitializeHook)<Data = any> = (data: Data) => void | Promise<void>

    The `initialize` hook provides a way to define a custom function that runs in the hooks thread when the hooks module is initialized. Initialization happens when the hooks module is registered via register.

    This hook can receive data from a register invocation, including ports and other transferable objects. The return value of `initialize` can be a `Promise`, in which case it will be awaited before the main application thread execution resumes.
  + type [LoadHook](https://bun.com/reference/node/module/default/LoadHook) = (url: string, context: [LoadHookContext](https://bun.com/reference/node/module/default/LoadHookContext), nextLoad: (url: string, context?: Partial<[LoadHookContext](https://bun.com/reference/node/module/default/LoadHookContext)>) => [LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput) | Promise<[LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput)>) => [LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput) | Promise<[LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput)>

    The `load` hook provides a way to define a custom method of determining how a URL should be interpreted, retrieved, and parsed. It is also in charge of validating the import attributes.
  + type [LoadHookSync](https://bun.com/reference/node/module/default/LoadHookSync) = (url: string, context: [LoadHookContext](https://bun.com/reference/node/module/default/LoadHookContext), nextLoad: (url: string, context?: Partial<[LoadHookContext](https://bun.com/reference/node/module/default/LoadHookContext)>) => [LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput)) => [LoadFnOutput](https://bun.com/reference/node/module/default/LoadFnOutput)
  + type [ModuleFormat](https://bun.com/reference/node/module/default/ModuleFormat) = 'addon' | 'builtin' | 'commonjs' | 'commonjs-typescript' | 'json' | 'module' | 'module-typescript' | 'wasm'
  + type [ModuleSource](https://bun.com/reference/node/module/default/ModuleSource) = string | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | NodeJS.TypedArray
  + type [ResolveHook](https://bun.com/reference/node/module/default/ResolveHook) = (specifier: string, context: [ResolveHookContext](https://bun.com/reference/node/module/default/ResolveHookContext), nextResolve: (specifier: string, context?: Partial<[ResolveHookContext](https://bun.com/reference/node/module/default/ResolveHookContext)>) => [ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput) | Promise<[ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput)>) => [ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput) | Promise<[ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput)>

    The `resolve` hook chain is responsible for telling Node.js where to find and how to cache a given `import` statement or expression, or `require` call. It can optionally return a format (such as `'module'`) as a hint to the `load` hook. If a format is specified, the `load` hook is ultimately responsible for providing the final `format` value (and it is free to ignore the hint provided by `resolve`); if `resolve` provides a `format`, a custom `load` hook is required even if only to pass the value to the Node.js default `load` hook.
  + type [ResolveHookSync](https://bun.com/reference/node/module/default/ResolveHookSync) = (specifier: string, context: [ResolveHookContext](https://bun.com/reference/node/module/default/ResolveHookContext), nextResolve: (specifier: string, context?: Partial<[ResolveHookContext](https://bun.com/reference/node/module/default/ResolveHookContext)>) => [ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput)) => [ResolveFnOutput](https://bun.com/reference/node/module/default/ResolveFnOutput)
  + const [builtinModules](https://bun.com/reference/node/module/default/builtinModules): readonly string[]

    A list of the names of all modules provided by Node.js. Can be used to verify if a module is maintained by a third party or not.

    Note: the list doesn't contain prefix-only modules like `node:test`.
  + function [createRequire](https://bun.com/reference/node/module/default/createRequire)(

    path: string | [URL](https://bun.com/reference/node/url/URL)

    ): Require;

    @param path

    Filename to be used to construct the require function. Must be a file URL object, file URL string, or absolute path string.
  + function [enableCompileCache](https://bun.com/reference/node/module/default/enableCompileCache)(

    cacheDir?: string

    ): [EnableCompileCacheResult](https://bun.com/reference/node/module/default/EnableCompileCacheResult);

    Enable [module compile cache](https://nodejs.org/docs/latest-v24.x/api/module.html#module-compile-cache) in the current Node.js instance.

    If `cacheDir` is not specified, Node.js will either use the directory specified by the `NODE_COMPILE_CACHE=dir` environment variable if it's set, or use `path.join(os.tmpdir(), 'node-compile-cache')` otherwise. For general use cases, it's recommended to call `module.enableCompileCache()` without specifying the `cacheDir`, so that the directory can be overridden by the `NODE_COMPILE_CACHE` environment variable when necessary.

    Since compile cache is supposed to be a quiet optimization that is not required for the application to be functional, this method is designed to not throw any exception when the compile cache cannot be enabled. Instead, it will return an object containing an error message in the `message` field to aid debugging. If compile cache is enabled successfully, the `directory` field in the returned object contains the path to the directory where the compile cache is stored. The `status` field in the returned object would be one of the `module.constants.compileCacheStatus` values to indicate the result of the attempt to enable the [module compile cache](https://nodejs.org/docs/latest-v24.x/api/module.html#module-compile-cache).

    This method only affects the current Node.js instance. To enable it in child worker threads, either call this method in child worker threads too, or set the `process.env.NODE_COMPILE_CACHE` value to compile cache directory so the behavior can be inherited into the child workers. The directory can be obtained either from the `directory` field returned by this method, or with getCompileCacheDir.

    @param cacheDir

    Optional path to specify the directory where the compile cache will be stored/retrieved.
  + function [findPackageJSON](https://bun.com/reference/node/module/default/findPackageJSON)(

    specifier: string | [URL](https://bun.com/reference/node/url/URL),

    base?: string | [URL](https://bun.com/reference/node/url/URL)

    ): undefined | string;

    ```
    /path/to/project
      ├ packages/
        ├ bar/
          ├ bar.js
          └ package.json // name = '@foo/bar'
        └ qux/
          ├ node_modules/
            └ some-package/
              └ package.json // name = 'some-package'
          ├ qux.js
          └ package.json // name = '@foo/qux'
      ├ main.js
      └ package.json // name = '@foo'
    ```

    ```
    // /path/to/project/packages/bar/bar.js
    import { findPackageJSON } from 'node:module';

    findPackageJSON('..', import.meta.url);
    // '/path/to/project/package.json'
    // Same result when passing an absolute specifier instead:
    findPackageJSON(new URL('../', import.meta.url));
    findPackageJSON(import.meta.resolve('../'));

    findPackageJSON('some-package', import.meta.url);
    // '/path/to/project/packages/bar/node_modules/some-package/package.json'
    // When passing an absolute specifier, you might get a different result if the
    // resolved module is inside a subfolder that has nested `package.json`.
    findPackageJSON(import.meta.resolve('some-package'));
    // '/path/to/project/packages/bar/node_modules/some-package/some-subfolder/package.json'

    findPackageJSON('@foo/qux', import.meta.url);
    // '/path/to/project/packages/qux/package.json'
    ```

    @param specifier

    The specifier for the module whose `package.json` to retrieve. When passing a *bare specifier*, the `package.json` at the root of the package is returned. When passing a *relative specifier* or an *absolute specifier*, the closest parent `package.json` is returned.

    @param base

    The absolute location (`file:` URL string or FS path) of the containing module. For CJS, use `__filename` (not `__dirname`!); for ESM, use `import.meta.url`. You do not need to pass it if `specifier` is an *absolute specifier*.

    @returns

    A path if the `package.json` is found. When `startLocation` is a package, the package's root `package.json`; when a relative or unresolved, the closest `package.json` to the `startLocation`.
  + function [findSourceMap](https://bun.com/reference/node/module/default/findSourceMap)(

    path: string

    ): undefined | [SourceMap](https://bun.com/reference/node/module/default/SourceMap);

    `path` is the resolved path for the file for which a corresponding source map should be fetched.

    @returns

    Returns `module.SourceMap` if a source map is found, `undefined` otherwise.
  + function [flushCompileCache](https://bun.com/reference/node/module/default/flushCompileCache)(): void;

    Flush the [module compile cache](https://nodejs.org/docs/latest-v24.x/api/module.html#module-compile-cache) accumulated from modules already loaded in the current Node.js instance to disk. This returns after all the flushing file system operations come to an end, no matter they succeed or not. If there are any errors, this will fail silently, since compile cache misses should not interfere with the actual operation of the application.
  + function [getCompileCacheDir](https://bun.com/reference/node/module/default/getCompileCacheDir)(): undefined | string;

    @returns

    Path to the [module compile cache](https://nodejs.org/docs/latest-v24.x/api/module.html#module-compile-cache) directory if it is enabled, or `undefined` otherwise.
  + function [getSourceMapsSupport](https://bun.com/reference/node/module/default/getSourceMapsSupport)(): [SourceMapsSupport](https://bun.com/reference/node/module/default/SourceMapsSupport);

    This method returns whether the [Source Map v3](https://tc39.es/ecma426/) support for stack traces is enabled.
  + function [isBuiltin](https://bun.com/reference/node/module/default/isBuiltin)(

    moduleName: string

    ): boolean;
  + function [register](https://bun.com/reference/node/module/default/register)<Data = any>(

    specifier: string | [URL](https://bun.com/reference/node/url/URL),

    parentURL?: string | [URL](https://bun.com/reference/node/url/URL),

    options?: [RegisterOptions](https://bun.com/reference/node/module/default/RegisterOptions)<Data>

    ): void;

    Register a module that exports hooks that customize Node.js module resolution and loading behavior. See [Customization hooks](https://nodejs.org/docs/latest-v24.x/api/module.html#customization-hooks).

    This feature requires `--allow-worker` if used with the [Permission Model](https://nodejs.org/docs/latest-v24.x/api/permissions.html#permission-model).

    @param specifier

    Customization hooks to be registered; this should be the same string that would be passed to `import()`, except that if it is relative, it is resolved relative to `parentURL`.

    @param parentURL

    f you want to resolve `specifier` relative to a base URL, such as `import.meta.url`, you can pass that URL here.

    function [register](https://bun.com/reference/node/module/default/register)<Data = any>(

    specifier: string | [URL](https://bun.com/reference/node/url/URL),

    options?: [RegisterOptions](https://bun.com/reference/node/module/default/RegisterOptions)<Data>

    ): void;

    Register a module that exports hooks that customize Node.js module resolution and loading behavior. See [Customization hooks](https://nodejs.org/docs/latest-v24.x/api/module.html#customization-hooks).

    This feature requires `--allow-worker` if used with the [Permission Model](https://nodejs.org/docs/latest-v24.x/api/permissions.html#permission-model).

    @param specifier

    Customization hooks to be registered; this should be the same string that would be passed to `import()`, except that if it is relative, it is resolved relative to `parentURL`.
  + function [registerHooks](https://bun.com/reference/node/module/default/registerHooks)(

    options: [RegisterHooksOptions](https://bun.com/reference/node/module/default/RegisterHooksOptions)

    ): [ModuleHooks](https://bun.com/reference/node/module/default/ModuleHooks);

    Register [hooks](https://nodejs.org/docs/latest-v24.x/api/module.html#customization-hooks) that customize Node.js module resolution and loading behavior.
  + function [runMain](https://bun.com/reference/node/module/default/runMain)(

    main?: string

    ): void;
  + function [setSourceMapsSupport](https://bun.com/reference/node/module/default/setSourceMapsSupport)(

    enabled: boolean,

    options?: [SetSourceMapsSupportOptions](https://bun.com/reference/node/module/default/SetSourceMapsSupportOptions)

    ): void;

    This function enables or disables the [Source Map v3](https://tc39.es/ecma426/) support for stack traces.

    It provides same features as launching Node.js process with commandline options `--enable-source-maps`, with additional options to alter the support for files in `node_modules` or generated codes.

    Only source maps in JavaScript files that are loaded after source maps has been enabled will be parsed and loaded. Preferably, use the commandline options `--enable-source-maps` to avoid losing track of source maps of modules loaded before this API call.
  + function [stripTypeScriptTypes](https://bun.com/reference/node/module/default/stripTypeScriptTypes)(

    code: string,

    options?: [StripTypeScriptTypesOptions](https://bun.com/reference/node/module/default/StripTypeScriptTypesOptions)

    ): string;

    `module.stripTypeScriptTypes()` removes type annotations from TypeScript code. It can be used to strip type annotations from TypeScript code before running it with `vm.runInContext()` or `vm.compileFunction()`. By default, it will throw an error if the code contains TypeScript features that require transformation such as `Enums`, see [type-stripping](https://nodejs.org/docs/latest-v24.x/api/typescript.md#type-stripping) for more information. When mode is `'transform'`, it also transforms TypeScript features to JavaScript, see [transform TypeScript features](https://nodejs.org/docs/latest-v24.x/api/typescript.md#typescript-features) for more information. When mode is `'strip'`, source maps are not generated, because locations are preserved. If `sourceMap` is provided, when mode is `'strip'`, an error will be thrown.

    *WARNING*: The output of this function should not be considered stable across Node.js versions, due to changes in the TypeScript parser.

    ```
    import { stripTypeScriptTypes } from 'node:module';
    const code = 'const a: number = 1;';
    const strippedCode = stripTypeScriptTypes(code);
    console.log(strippedCode);
    // Prints: const a         = 1;
    ```

    If `sourceUrl` is provided, it will be used appended as a comment at the end of the output:

    ```
    import { stripTypeScriptTypes } from 'node:module';
    const code = 'const a: number = 1;';
    const strippedCode = stripTypeScriptTypes(code, { mode: 'strip', sourceUrl: 'source.ts' });
    console.log(strippedCode);
    // Prints: const a         = 1\n\n//# sourceURL=source.ts;
    ```

    When `mode` is `'transform'`, the code is transformed to JavaScript:

    ```
    import { stripTypeScriptTypes } from 'node:module';
    const code = `
      namespace MathUtil {
        export const add = (a: number, b: number) => a + b;
      }`;
    const strippedCode = stripTypeScriptTypes(code, { mode: 'transform', sourceMap: true });
    console.log(strippedCode);
    // Prints:
    // var MathUtil;
    // (function(MathUtil) {
    //     MathUtil.add = (a, b)=>a + b;
    // })(MathUtil || (MathUtil = {}));
    // # sourceMappingURL=data:application/json;base64, ...
    ```

    @param code

    The code to strip type annotations from.

    @returns

    The code with type annotations stripped.
  + function [syncBuiltinESMExports](https://bun.com/reference/node/module/default/syncBuiltinESMExports)(): void;

    The `module.syncBuiltinESMExports()` method updates all the live bindings for builtin `ES Modules` to match the properties of the `CommonJS` exports. It does not add or remove exported names from the `ES Modules`.

    ```
    import fs from 'node:fs';
    import assert from 'node:assert';
    import { syncBuiltinESMExports } from 'node:module';

    fs.readFile = newAPI;

    delete fs.readFileSync;

    function newAPI() {
      // ...
    }

    fs.newAPI = newAPI;

    syncBuiltinESMExports();

    import('node:fs').then((esmFS) => {
      // It syncs the existing readFile property with the new value
      assert.strictEqual(esmFS.readFile, newAPI);
      // readFileSync has been deleted from the required fs
      assert.strictEqual('readFileSync' in fs, false);
      // syncBuiltinESMExports() does not remove readFileSync from esmFS
      assert.strictEqual('readFileSync' in esmFS, true);
      // syncBuiltinESMExports() does not add names
      assert.strictEqual(esmFS.newAPI, undefined);
    });
    ```
  + function [wrap](https://bun.com/reference/node/module/default/wrap)(

    script: string

    ): string;
* ### class [default](https://bun.com/reference/node/module/default)

  + [children](https://bun.com/reference/node/module/default/children): Module[]

    The module objects required for the first time by this one.
  + [exports](https://bun.com/reference/node/module/default/exports): any

    The `module.exports` object is created by the `Module` system. Sometimes this is not acceptable; many want their module to be an instance of some class. To do this, assign the desired export object to `module.exports`.
  + [filename](https://bun.com/reference/node/module/default/filename): string

    The fully resolved filename of the module.
  + [id](https://bun.com/reference/node/module/default/id): string

    The identifier for the module. Typically this is the fully resolved filename.
  + [isPreloading](https://bun.com/reference/node/module/default/isPreloading): boolean

    `true` if the module is running during the Node.js preload phase.
  + [loaded](https://bun.com/reference/node/module/default/loaded): boolean

    Whether or not the module is done loading, or is in the process of loading.
  + [path](https://bun.com/reference/node/module/default/path): string

    The directory name of the module. This is usually the same as the `path.dirname()` of the `module.id`.
  + [paths](https://bun.com/reference/node/module/default/paths): string[]

    The search paths for the module.
  + [require](https://bun.com/reference/node/module/default/require)(

    id: string

    ): any;

    The `module.require()` method provides a way to load a module as if `require()` was called from the original module.