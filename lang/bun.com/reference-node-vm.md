---
url: https://bun.com/reference/node/vm
title: Node.js vm module | API Reference | Bun
source_domain: bun.com
---

# Node.js vm module | API Reference | Bun

Node.js module

# [vm](https://bun.com/reference/node/vm)

The `'node:vm'` module provides APIs to compile and run code within V8 virtual machines contexts. It includes `Script`, `createContext`, and `runInContext` functions.

Use it to sandbox code execution, evaluate untrusted scripts safely, or preload global variables in isolated contexts.

Works in Bun

Core script execution functionality works. Experimental VM ES Modules (`vm.Module`, etc.) and the `importModuleDynamically` hook are not implemented. Several options like `timeout`, `breakOnSigint`, and `cachedData` are also not yet implemented.

* ### namespace [constants](https://bun.com/reference/node/vm/constants)

  Returns an object containing commonly used constants for VM operations.

  + const [DONT\_CONTEXTIFY](https://bun.com/reference/node/vm/constants/DONT_CONTEXTIFY): number

    This constant, when used as the `contextObject` argument in vm APIs, instructs Node.js to create a context without wrapping its global object with another object in a Node.js-specific manner. As a result, the `globalThis` value inside the new context would behave more closely to an ordinary one.

    When `vm.constants.DONT_CONTEXTIFY` is used as the `contextObject` argument to createContext, the returned object is a proxy-like object to the global object in the newly created context with fewer Node.js-specific quirks. It is reference equal to the `globalThis` value in the new context, can be modified from outside the context, and can be used to access built-ins in the new context directly.
  + const [USE\_MAIN\_CONTEXT\_DEFAULT\_LOADER](https://bun.com/reference/node/vm/constants/USE_MAIN_CONTEXT_DEFAULT_LOADER): number

    A constant that can be used as the `importModuleDynamically` option to `vm.Script` and `vm.compileFunction()` so that Node.js uses the default ESM loader from the main context to load the requested module.

    For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
* ### class [Module](https://bun.com/reference/node/vm/Module)

  This feature is only available with the `--experimental-vm-modules` command flag enabled.

  The `vm.Module` class provides a low-level interface for using ECMAScript modules in VM contexts. It is the counterpart of the `vm.Script` class that closely mirrors [Module Record](https://tc39.es/ecma262/#sec-abstract-module-records)s as defined in the ECMAScript specification.

  Unlike `vm.Script` however, every `vm.Module` object is bound to a context from its creation.

  Using a `vm.Module` object requires three distinct steps: creation/parsing, linking, and evaluation. These three steps are illustrated in the following example.

  This implementation lies at a lower level than the `ECMAScript Module loader`. There is also no way to interact with the Loader yet, though support is planned.

  ```
  import vm from 'node:vm';

  const contextifiedObject = vm.createContext({
    secret: 42,
    print: console.log,
  });

  // Step 1
  //
  // Create a Module by constructing a new `vm.SourceTextModule` object. This
  // parses the provided source text, throwing a `SyntaxError` if anything goes
  // wrong. By default, a Module is created in the top context. But here, we
  // specify `contextifiedObject` as the context this Module belongs to.
  //
  // Here, we attempt to obtain the default export from the module "foo", and
  // put it into local binding "secret".

  const rootModule = new vm.SourceTextModule(`
    import s from 'foo';
    s;
    print(s);
  `, { context: contextifiedObject });

  // Step 2
  //
  // "Link" the imported dependencies of this Module to it.
  //
  // Obtain the requested dependencies of a SourceTextModule by
  // `sourceTextModule.moduleRequests` and resolve them.
  //
  // Even top-level Modules without dependencies must be explicitly linked. The
  // array passed to `sourceTextModule.linkRequests(modules)` can be
  // empty, however.
  //
  // Note: This is a contrived example in that the resolveAndLinkDependencies
  // creates a new "foo" module every time it is called. In a full-fledged
  // module system, a cache would probably be used to avoid duplicated modules.

  const moduleMap = new Map([
    ['root', rootModule],
  ]);

  function resolveAndLinkDependencies(module) {
    const requestedModules = module.moduleRequests.map((request) => {
      // In a full-fledged module system, the resolveAndLinkDependencies would
      // resolve the module with the module cache key `[specifier, attributes]`.
      // In this example, we just use the specifier as the key.
      const specifier = request.specifier;

      let requestedModule = moduleMap.get(specifier);
      if (requestedModule === undefined) {
        requestedModule = new vm.SourceTextModule(`
          // The "secret" variable refers to the global variable we added to
          // "contextifiedObject" when creating the context.
          export default secret;
        `, { context: referencingModule.context });
        moduleMap.set(specifier, linkedModule);
        // Resolve the dependencies of the new module as well.
        resolveAndLinkDependencies(requestedModule);
      }

      return requestedModule;
    });

    module.linkRequests(requestedModules);
  }

  resolveAndLinkDependencies(rootModule);
  rootModule.instantiate();

  // Step 3
  //
  // Evaluate the Module. The evaluate() method returns a promise which will
  // resolve after the module has finished evaluating.

  // Prints 42.
  await rootModule.evaluate();
  ```

  + [context](https://bun.com/reference/node/vm/Module/context): [Context](https://bun.com/reference/node/vm/Context)
  + [error](https://bun.com/reference/node/vm/Module/error): any

    If the `module.status` is `'errored'`, this property contains the exception thrown by the module during evaluation. If the status is anything else, accessing this property will result in a thrown exception.

    The value `undefined` cannot be used for cases where there is not a thrown exception due to possible ambiguity with `throw undefined;`.

    Corresponds to the `[[EvaluationError]]` field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
  + [identifier](https://bun.com/reference/node/vm/Module/identifier): string

    The identifier of the current module, as set in the constructor.
  + [namespace](https://bun.com/reference/node/vm/Module/namespace): Object

    The namespace object of the module. This is only available after linking (`module.link()`) has completed.

    Corresponds to the [GetModuleNamespace](https://tc39.es/ecma262/#sec-getmodulenamespace) abstract operation in the ECMAScript specification.
  + [status](https://bun.com/reference/node/vm/Module/status): [ModuleStatus](https://bun.com/reference/node/vm/ModuleStatus)

    The current status of the module. Will be one of:

    - `'unlinked'`: `module.link()` has not yet been called.
    - `'linking'`: `module.link()` has been called, but not all Promises returned by the linker function have been resolved yet.
    - `'linked'`: The module has been linked successfully, and all of its dependencies are linked, but `module.evaluate()` has not yet been called.
    - `'evaluating'`: The module is being evaluated through a `module.evaluate()` on itself or a parent module.
    - `'evaluated'`: The module has been successfully evaluated.
    - `'errored'`: The module has been evaluated, but an exception was thrown.

    Other than `'errored'`, this status string corresponds to the specification's [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records)'s `[[Status]]` field. `'errored'` corresponds to `'evaluated'` in the specification, but with `[[EvaluationError]]` set to a value that is not `undefined`.
  + [evaluate](https://bun.com/reference/node/vm/Module/evaluate)(

    options?: [ModuleEvaluateOptions](https://bun.com/reference/node/vm/ModuleEvaluateOptions)

    ): Promise<void>;

    Evaluate the module.

    This must be called after the module has been linked; otherwise it will reject. It could be called also when the module has already been evaluated, in which case it will either do nothing if the initial evaluation ended in success (`module.status` is `'evaluated'`) or it will re-throw the exception that the initial evaluation resulted in (`module.status` is `'errored'`).

    This method cannot be called while the module is being evaluated (`module.status` is `'evaluating'`).

    Corresponds to the [Evaluate() concrete method](https://tc39.es/ecma262/#sec-moduleevaluation) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.

    @returns

    Fulfills with `undefined` upon success.
  + [link](https://bun.com/reference/node/vm/Module/link)(

    linker: [ModuleLinker](https://bun.com/reference/node/vm/ModuleLinker)

    ): Promise<void>;

    Link module dependencies. This method must be called before evaluation, and can only be called once per module.

    Use `sourceTextModule.linkRequests(modules)` and `sourceTextModule.instantiate()` to link modules either synchronously or asynchronously.

    The function is expected to return a `Module` object or a `Promise` that eventually resolves to a `Module` object. The returned `Module` must satisfy the following two invariants:

    - It must belong to the same context as the parent `Module`.
    - Its `status` must not be `'errored'`.

    If the returned `Module`'s `status` is `'unlinked'`, this method will be recursively called on the returned `Module` with the same provided `linker` function.

    `link()` returns a `Promise` that will either get resolved when all linking instances resolve to a valid `Module`, or rejected if the linker function either throws an exception or returns an invalid `Module`.

    The linker function roughly corresponds to the implementation-defined [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) abstract operation in the ECMAScript specification, with a few key differences:

    - The linker function is allowed to be asynchronous while [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) is synchronous.

    The actual [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation used during module linking is one that returns the modules linked during linking. Since at that point all modules would have been fully linked already, the [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation is fully synchronous per specification.

    Corresponds to the [Link() concrete method](https://tc39.es/ecma262/#sec-moduledeclarationlinking) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
* ### class [Script](https://bun.com/reference/node/vm/Script)

  Instances of the `vm.Script` class contain precompiled scripts that can be executed in specific contexts.

  + [cachedData](https://bun.com/reference/node/vm/Script/cachedData)?: NonSharedBuffer
  + [cachedDataRejected](https://bun.com/reference/node/vm/Script/cachedDataRejected)?: boolean

    When `cachedData` is supplied to create the `vm.Script`, this value will be set to either `true` or `false` depending on acceptance of the data by V8. Otherwise the value is `undefined`.
  + [sourceMapURL](https://bun.com/reference/node/vm/Script/sourceMapURL): undefined | string

    When the script is compiled from a source that contains a source map magic comment, this property will be set to the URL of the source map.

    ```
    import vm from 'node:vm';

    const script = new vm.Script(`
    function myFunc() {}
    //# sourceMappingURL=sourcemap.json
    `);

    console.log(script.sourceMapURL);
    // Prints: sourcemap.json
    ```
  + [createCachedData](https://bun.com/reference/node/vm/Script/createCachedData)(): NonSharedBuffer;

    Creates a code cache that can be used with the `Script` constructor's `cachedData` option. Returns a `Buffer`. This method may be called at any time and any number of times.

    The code cache of the `Script` doesn't contain any JavaScript observable states. The code cache is safe to be saved along side the script source and used to construct new `Script` instances multiple times.

    Functions in the `Script` source can be marked as lazily compiled and they are not compiled at construction of the `Script`. These functions are going to be compiled when they are invoked the first time. The code cache serializes the metadata that V8 currently knows about the `Script` that it can use to speed up future compilations.

    ```
    const script = new vm.Script(`
    function add(a, b) {
      return a + b;
    }

    const x = add(1, 2);
    `);

    const cacheWithoutAdd = script.createCachedData();
    // In `cacheWithoutAdd` the function `add()` is marked for full compilation
    // upon invocation.

    script.runInThisContext();

    const cacheWithAdd = script.createCachedData();
    // `cacheWithAdd` contains fully compiled function `add()`.
    ```
  + [runInContext](https://bun.com/reference/node/vm/Script/runInContext)(

    contextifiedObject: [Context](https://bun.com/reference/node/vm/Context),

    options?: [RunningScriptOptions](https://bun.com/reference/node/vm/RunningScriptOptions)

    ): any;

    Runs the compiled code contained by the `vm.Script` object within the given `contextifiedObject` and returns the result. Running code does not have access to local scope.

    The following example compiles code that increments a global variable, sets the value of another global variable, then execute the code multiple times. The globals are contained in the `context` object.

    ```
    import vm from 'node:vm';

    const context = {
      animal: 'cat',
      count: 2,
    };

    const script = new vm.Script('count += 1; name = "kitty";');

    vm.createContext(context);
    for (let i = 0; i < 10; ++i) {
      script.runInContext(context);
    }

    console.log(context);
    // Prints: { animal: 'cat', count: 12, name: 'kitty' }
    ```

    Using the `timeout` or `breakOnSigint` options will result in new event loops and corresponding threads being started, which have a non-zero performance overhead.

    @param contextifiedObject

    A `contextified` object as returned by the `vm.createContext()` method.

    @returns

    the result of the very last statement executed in the script.
  + [runInNewContext](https://bun.com/reference/node/vm/Script/runInNewContext)(

    contextObject?: number | [Context](https://bun.com/reference/node/vm/Context),

    options?: [RunningScriptInNewContextOptions](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions)

    ): any;

    This method is a shortcut to `script.runInContext(vm.createContext(options), options)`. It does several things at once:

    1. Creates a new context.
    2. If `contextObject` is an object, contextifies it with the new context. If `contextObject` is undefined, creates a new object and contextifies it. If `contextObject` is `vm.constants.DONT_CONTEXTIFY`, don't contextify anything.
    3. Runs the compiled code contained by the `vm.Script` object within the created context. The code does not have access to the scope in which this method is called.
    4. Returns the result.

    The following example compiles code that sets a global variable, then executes the code multiple times in different contexts. The globals are set on and contained within each individual `context`.

    ```
    const vm = require('node:vm');

    const script = new vm.Script('globalVar = "set"');

    const contexts = [{}, {}, {}];
    contexts.forEach((context) => {
      script.runInNewContext(context);
    });

    console.log(contexts);
    // Prints: [{ globalVar: 'set' }, { globalVar: 'set' }, { globalVar: 'set' }]

    // This would throw if the context is created from a contextified object.
    // vm.constants.DONT_CONTEXTIFY allows creating contexts with ordinary
    // global objects that can be frozen.
    const freezeScript = new vm.Script('Object.freeze(globalThis); globalThis;');
    const frozenContext = freezeScript.runInNewContext(vm.constants.DONT_CONTEXTIFY);
    ```

    @param contextObject

    Either `vm.constants.DONT_CONTEXTIFY` or an object that will be contextified. If `undefined`, an empty contextified object will be created for backwards compatibility.

    @returns

    the result of the very last statement executed in the script.
  + [runInThisContext](https://bun.com/reference/node/vm/Script/runInThisContext)(

    options?: [RunningScriptOptions](https://bun.com/reference/node/vm/RunningScriptOptions)

    ): any;

    Runs the compiled code contained by the `vm.Script` within the context of the current `global` object. Running code does not have access to local scope, but *does* have access to the current `global` object.

    The following example compiles code that increments a `global` variable then executes that code multiple times:

    ```
    import vm from 'node:vm';

    global.globalVar = 0;

    const script = new vm.Script('globalVar += 1', { filename: 'myfile.vm' });

    for (let i = 0; i < 1000; ++i) {
      script.runInThisContext();
    }

    console.log(globalVar);

    // 1000
    ```

    @returns

    the result of the very last statement executed in the script.
* ### class [SourceTextModule](https://bun.com/reference/node/vm/SourceTextModule)

  This feature is only available with the `--experimental-vm-modules` command flag enabled.

  The `vm.SourceTextModule` class provides the [Source Text Module Record](https://tc39.es/ecma262/#sec-source-text-module-records) as defined in the ECMAScript specification.

  + [context](https://bun.com/reference/node/vm/SourceTextModule/context): [Context](https://bun.com/reference/node/vm/Context)
  + [error](https://bun.com/reference/node/vm/SourceTextModule/error): any

    If the `module.status` is `'errored'`, this property contains the exception thrown by the module during evaluation. If the status is anything else, accessing this property will result in a thrown exception.

    The value `undefined` cannot be used for cases where there is not a thrown exception due to possible ambiguity with `throw undefined;`.

    Corresponds to the `[[EvaluationError]]` field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
  + [identifier](https://bun.com/reference/node/vm/SourceTextModule/identifier): string

    The identifier of the current module, as set in the constructor.
  + readonly [moduleRequests](https://bun.com/reference/node/vm/SourceTextModule/moduleRequests): readonly [ModuleRequest](https://bun.com/reference/node/vm/ModuleRequest)[]

    The requested import dependencies of this module. The returned array is frozen to disallow any changes to it.

    For example, given a source text:

    ```
    import foo from 'foo';
    import fooAlias from 'foo';
    import bar from './bar.js';
    import withAttrs from '../with-attrs.ts' with { arbitraryAttr: 'attr-val' };
    import source Module from 'wasm-mod.wasm';
    ```

    The value of the `sourceTextModule.moduleRequests` will be:

    ```
    [
      {
        specifier: 'foo',
        attributes: {},
        phase: 'evaluation',
      },
      {
        specifier: 'foo',
        attributes: {},
        phase: 'evaluation',
      },
      {
        specifier: './bar.js',
        attributes: {},
        phase: 'evaluation',
      },
      {
        specifier: '../with-attrs.ts',
        attributes: { arbitraryAttr: 'attr-val' },
        phase: 'evaluation',
      },
      {
        specifier: 'wasm-mod.wasm',
        attributes: {},
        phase: 'source',
      },
    ];
    ```
  + [namespace](https://bun.com/reference/node/vm/SourceTextModule/namespace): Object

    The namespace object of the module. This is only available after linking (`module.link()`) has completed.

    Corresponds to the [GetModuleNamespace](https://tc39.es/ecma262/#sec-getmodulenamespace) abstract operation in the ECMAScript specification.
  + [status](https://bun.com/reference/node/vm/SourceTextModule/status): [ModuleStatus](https://bun.com/reference/node/vm/ModuleStatus)

    The current status of the module. Will be one of:

    - `'unlinked'`: `module.link()` has not yet been called.
    - `'linking'`: `module.link()` has been called, but not all Promises returned by the linker function have been resolved yet.
    - `'linked'`: The module has been linked successfully, and all of its dependencies are linked, but `module.evaluate()` has not yet been called.
    - `'evaluating'`: The module is being evaluated through a `module.evaluate()` on itself or a parent module.
    - `'evaluated'`: The module has been successfully evaluated.
    - `'errored'`: The module has been evaluated, but an exception was thrown.

    Other than `'errored'`, this status string corresponds to the specification's [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records)'s `[[Status]]` field. `'errored'` corresponds to `'evaluated'` in the specification, but with `[[EvaluationError]]` set to a value that is not `undefined`.
  + [evaluate](https://bun.com/reference/node/vm/SourceTextModule/evaluate)(

    options?: [ModuleEvaluateOptions](https://bun.com/reference/node/vm/ModuleEvaluateOptions)

    ): Promise<void>;

    Evaluate the module.

    This must be called after the module has been linked; otherwise it will reject. It could be called also when the module has already been evaluated, in which case it will either do nothing if the initial evaluation ended in success (`module.status` is `'evaluated'`) or it will re-throw the exception that the initial evaluation resulted in (`module.status` is `'errored'`).

    This method cannot be called while the module is being evaluated (`module.status` is `'evaluating'`).

    Corresponds to the [Evaluate() concrete method](https://tc39.es/ecma262/#sec-moduleevaluation) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.

    @returns

    Fulfills with `undefined` upon success.
  + [hasAsyncGraph](https://bun.com/reference/node/vm/SourceTextModule/hasAsyncGraph)(): boolean;

    Iterates over the dependency graph and returns `true` if any module in its dependencies or this module itself contains top-level `await` expressions, otherwise returns `false`.

    The search may be slow if the graph is big enough.

    This requires the module to be instantiated first. If the module is not instantiated yet, an error will be thrown.
  + [hasTopLevelAwait](https://bun.com/reference/node/vm/SourceTextModule/hasTopLevelAwait)(): boolean;

    Returns whether the module itself contains any top-level `await` expressions.

    This corresponds to the field `[[HasTLA]]` in [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) in the ECMAScript specification.
  + [instantiate](https://bun.com/reference/node/vm/SourceTextModule/instantiate)(): void;

    Instantiate the module with the linked requested modules.

    This resolves the imported bindings of the module, including re-exported binding names. When there are any bindings that cannot be resolved, an error would be thrown synchronously.

    If the requested modules include cyclic dependencies, the `sourceTextModule.linkRequests(modules)` method must be called on all modules in the cycle before calling this method.
  + [link](https://bun.com/reference/node/vm/SourceTextModule/link)(

    linker: [ModuleLinker](https://bun.com/reference/node/vm/ModuleLinker)

    ): Promise<void>;

    Link module dependencies. This method must be called before evaluation, and can only be called once per module.

    Use `sourceTextModule.linkRequests(modules)` and `sourceTextModule.instantiate()` to link modules either synchronously or asynchronously.

    The function is expected to return a `Module` object or a `Promise` that eventually resolves to a `Module` object. The returned `Module` must satisfy the following two invariants:

    - It must belong to the same context as the parent `Module`.
    - Its `status` must not be `'errored'`.

    If the returned `Module`'s `status` is `'unlinked'`, this method will be recursively called on the returned `Module` with the same provided `linker` function.

    `link()` returns a `Promise` that will either get resolved when all linking instances resolve to a valid `Module`, or rejected if the linker function either throws an exception or returns an invalid `Module`.

    The linker function roughly corresponds to the implementation-defined [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) abstract operation in the ECMAScript specification, with a few key differences:

    - The linker function is allowed to be asynchronous while [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) is synchronous.

    The actual [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation used during module linking is one that returns the modules linked during linking. Since at that point all modules would have been fully linked already, the [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation is fully synchronous per specification.

    Corresponds to the [Link() concrete method](https://tc39.es/ecma262/#sec-moduledeclarationlinking) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
  + [linkRequests](https://bun.com/reference/node/vm/SourceTextModule/linkRequests)(

    modules: readonly [Module](https://bun.com/reference/node/vm/Module)[]

    ): void;

    Link module dependencies. This method must be called before evaluation, and can only be called once per module.

    The order of the module instances in the `modules` array should correspond to the order of `sourceTextModule.moduleRequests` being resolved. If two module requests have the same specifier and import attributes, they must be resolved with the same module instance or an `ERR_MODULE_LINK_MISMATCH` would be thrown. For example, when linking requests for this module:

    ```
    import foo from 'foo';
    import source Foo from 'foo';
    ```

    The `modules` array must contain two references to the same instance, because the two module requests are identical but in two phases.

    If the module has no dependencies, the `modules` array can be empty.

    Users can use `sourceTextModule.moduleRequests` to implement the host-defined [HostLoadImportedModule](https://tc39.es/ecma262/#sec-HostLoadImportedModule) abstract operation in the ECMAScript specification, and using `sourceTextModule.linkRequests()` to invoke specification defined [FinishLoadingImportedModule](https://tc39.es/ecma262/#sec-FinishLoadingImportedModule), on the module with all dependencies in a batch.

    It's up to the creator of the `SourceTextModule` to determine if the resolution of the dependencies is synchronous or asynchronous.

    After each module in the `modules` array is linked, call `sourceTextModule.instantiate()`.

    @param modules

    Array of `vm.Module` objects that this module depends on. The order of the modules in the array is the order of `sourceTextModule.moduleRequests`.
* ### class [SyntheticModule](https://bun.com/reference/node/vm/SyntheticModule)

  This feature is only available with the `--experimental-vm-modules` command flag enabled.

  The `vm.SyntheticModule` class provides the [Synthetic Module Record](https://heycam.github.io/webidl/#synthetic-module-records) as defined in the WebIDL specification. The purpose of synthetic modules is to provide a generic interface for exposing non-JavaScript sources to ECMAScript module graphs.

  ```
  import vm from 'node:vm';

  const source = '{ "a": 1 }';
  const module = new vm.SyntheticModule(['default'], function() {
    const obj = JSON.parse(source);
    this.setExport('default', obj);
  });

  // Use `module` in linking...
  ```

  + [context](https://bun.com/reference/node/vm/SyntheticModule/context): [Context](https://bun.com/reference/node/vm/Context)
  + [error](https://bun.com/reference/node/vm/SyntheticModule/error): any

    If the `module.status` is `'errored'`, this property contains the exception thrown by the module during evaluation. If the status is anything else, accessing this property will result in a thrown exception.

    The value `undefined` cannot be used for cases where there is not a thrown exception due to possible ambiguity with `throw undefined;`.

    Corresponds to the `[[EvaluationError]]` field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
  + [identifier](https://bun.com/reference/node/vm/SyntheticModule/identifier): string

    The identifier of the current module, as set in the constructor.
  + [namespace](https://bun.com/reference/node/vm/SyntheticModule/namespace): Object

    The namespace object of the module. This is only available after linking (`module.link()`) has completed.

    Corresponds to the [GetModuleNamespace](https://tc39.es/ecma262/#sec-getmodulenamespace) abstract operation in the ECMAScript specification.
  + [status](https://bun.com/reference/node/vm/SyntheticModule/status): [ModuleStatus](https://bun.com/reference/node/vm/ModuleStatus)

    The current status of the module. Will be one of:

    - `'unlinked'`: `module.link()` has not yet been called.
    - `'linking'`: `module.link()` has been called, but not all Promises returned by the linker function have been resolved yet.
    - `'linked'`: The module has been linked successfully, and all of its dependencies are linked, but `module.evaluate()` has not yet been called.
    - `'evaluating'`: The module is being evaluated through a `module.evaluate()` on itself or a parent module.
    - `'evaluated'`: The module has been successfully evaluated.
    - `'errored'`: The module has been evaluated, but an exception was thrown.

    Other than `'errored'`, this status string corresponds to the specification's [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records)'s `[[Status]]` field. `'errored'` corresponds to `'evaluated'` in the specification, but with `[[EvaluationError]]` set to a value that is not `undefined`.
  + [evaluate](https://bun.com/reference/node/vm/SyntheticModule/evaluate)(

    options?: [ModuleEvaluateOptions](https://bun.com/reference/node/vm/ModuleEvaluateOptions)

    ): Promise<void>;

    Evaluate the module.

    This must be called after the module has been linked; otherwise it will reject. It could be called also when the module has already been evaluated, in which case it will either do nothing if the initial evaluation ended in success (`module.status` is `'evaluated'`) or it will re-throw the exception that the initial evaluation resulted in (`module.status` is `'errored'`).

    This method cannot be called while the module is being evaluated (`module.status` is `'evaluating'`).

    Corresponds to the [Evaluate() concrete method](https://tc39.es/ecma262/#sec-moduleevaluation) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.

    @returns

    Fulfills with `undefined` upon success.
  + [link](https://bun.com/reference/node/vm/SyntheticModule/link)(

    linker: [ModuleLinker](https://bun.com/reference/node/vm/ModuleLinker)

    ): Promise<void>;

    Link module dependencies. This method must be called before evaluation, and can only be called once per module.

    Use `sourceTextModule.linkRequests(modules)` and `sourceTextModule.instantiate()` to link modules either synchronously or asynchronously.

    The function is expected to return a `Module` object or a `Promise` that eventually resolves to a `Module` object. The returned `Module` must satisfy the following two invariants:

    - It must belong to the same context as the parent `Module`.
    - Its `status` must not be `'errored'`.

    If the returned `Module`'s `status` is `'unlinked'`, this method will be recursively called on the returned `Module` with the same provided `linker` function.

    `link()` returns a `Promise` that will either get resolved when all linking instances resolve to a valid `Module`, or rejected if the linker function either throws an exception or returns an invalid `Module`.

    The linker function roughly corresponds to the implementation-defined [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) abstract operation in the ECMAScript specification, with a few key differences:

    - The linker function is allowed to be asynchronous while [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) is synchronous.

    The actual [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation used during module linking is one that returns the modules linked during linking. Since at that point all modules would have been fully linked already, the [HostResolveImportedModule](https://tc39.es/ecma262/#sec-hostresolveimportedmodule) implementation is fully synchronous per specification.

    Corresponds to the [Link() concrete method](https://tc39.es/ecma262/#sec-moduledeclarationlinking) field of [Cyclic Module Record](https://tc39.es/ecma262/#sec-cyclic-module-records) s in the ECMAScript specification.
  + [setExport](https://bun.com/reference/node/vm/SyntheticModule/setExport)(

    name: string,

    value: any

    ): void;

    This method sets the module export binding slots with the given value.

    ```
    import vm from 'node:vm';

    const m = new vm.SyntheticModule(['x'], () => {
      m.setExport('x', 1);
    });

    await m.evaluate();

    assert.strictEqual(m.namespace.x, 1);
    ```

    @param name

    Name of the export to set.

    @param value

    The value to set the export to.
* function [compileFunction](https://bun.com/reference/node/vm/compileFunction)(

  code: string,

  params?: readonly string[],

  options?: [CompileFunctionOptions](https://bun.com/reference/node/vm/CompileFunctionOptions)

  ): Function & Pick<[Script](https://bun.com/reference/node/vm/Script), 'cachedData' | 'cachedDataProduced' | 'cachedDataRejected'>;

  Compiles the given code into the provided context (if no context is supplied, the current context is used), and returns it wrapped inside a function with the given `params`.

  @param code

  The body of the function to compile.

  @param params

  An array of strings containing all parameters for the function.
* function [createContext](https://bun.com/reference/node/vm/createContext)(

  contextObject?: number | [Context](https://bun.com/reference/node/vm/Context),

  options?: [CreateContextOptions](https://bun.com/reference/node/vm/CreateContextOptions)

  ): [Context](https://bun.com/reference/node/vm/Context);

  If the given `contextObject` is an object, the `vm.createContext()` method will [prepare that object](https://nodejs.org/docs/latest-v24.x/api/vm.html#what-does-it-mean-to-contextify-an-object) and return a reference to it so that it can be used in calls to runInContext or [`script.runInContext()`](https://nodejs.org/docs/latest-v24.x/api/vm.html#scriptrunincontextcontextifiedobject-options). Inside such scripts, the global object will be wrapped by the `contextObject`, retaining all of its existing properties but also having the built-in objects and functions any standard [global object](https://es5.github.io/#x15.1) has. Outside of scripts run by the vm module, global variables will remain unchanged.

  ```
  const vm = require('node:vm');

  global.globalVar = 3;

  const context = { globalVar: 1 };
  vm.createContext(context);

  vm.runInContext('globalVar *= 2;', context);

  console.log(context);
  // Prints: { globalVar: 2 }

  console.log(global.globalVar);
  // Prints: 3
  ```

  If `contextObject` is omitted (or passed explicitly as `undefined`), a new, empty contextified object will be returned.

  When the global object in the newly created context is contextified, it has some quirks compared to ordinary global objects. For example, it cannot be frozen. To create a context without the contextifying quirks, pass `vm.constants.DONT_CONTEXTIFY` as the `contextObject` argument. See the documentation of `vm.constants.DONT_CONTEXTIFY` for details.

  The `vm.createContext()` method is primarily useful for creating a single context that can be used to run multiple scripts. For instance, if emulating a web browser, the method can be used to create a single context representing a window's global object, then run all `<script>` tags together within that context.

  The provided `name` and `origin` of the context are made visible through the Inspector API.

  @param contextObject

  Either `vm.constants.DONT_CONTEXTIFY` or an object that will be contextified. If `undefined`, an empty contextified object will be created for backwards compatibility.

  @returns

  contextified object.
* function [isContext](https://bun.com/reference/node/vm/isContext)(

  sandbox: [Context](https://bun.com/reference/node/vm/Context)

  ): boolean;

  Returns `true` if the given `object` object has been contextified using createContext, or if it's the global object of a context created using `vm.constants.DONT_CONTEXTIFY`.
* function [measureMemory](https://bun.com/reference/node/vm/measureMemory)(

  options?: [MeasureMemoryOptions](https://bun.com/reference/node/vm/MeasureMemoryOptions)

  ): Promise<[MemoryMeasurement](https://bun.com/reference/node/vm/MemoryMeasurement)>;

  Measure the memory known to V8 and used by all contexts known to the current V8 isolate, or the main context.

  The format of the object that the returned Promise may resolve with is specific to the V8 engine and may change from one version of V8 to the next.

  The returned result is different from the statistics returned by `v8.getHeapSpaceStatistics()` in that `vm.measureMemory()` measure the memory reachable by each V8 specific contexts in the current instance of the V8 engine, while the result of `v8.getHeapSpaceStatistics()` measure the memory occupied by each heap space in the current V8 instance.

  ```
  import vm from 'node:vm';
  // Measure the memory used by the main context.
  vm.measureMemory({ mode: 'summary' })
    // This is the same as vm.measureMemory()
    .then((result) => {
      // The current format is:
      // {
      //   total: {
      //      jsMemoryEstimate: 2418479, jsMemoryRange: [ 2418479, 2745799 ]
      //    }
      // }
      console.log(result);
    });

  const context = vm.createContext({ a: 1 });
  vm.measureMemory({ mode: 'detailed', execution: 'eager' })
    .then((result) => {
      // Reference the context here so that it won't be GC'ed
      // until the measurement is complete.
      console.log(context.a);
      // {
      //   total: {
      //     jsMemoryEstimate: 2574732,
      //     jsMemoryRange: [ 2574732, 2904372 ]
      //   },
      //   current: {
      //     jsMemoryEstimate: 2438996,
      //     jsMemoryRange: [ 2438996, 2768636 ]
      //   },
      //   other: [
      //     {
      //       jsMemoryEstimate: 135736,
      //       jsMemoryRange: [ 135736, 465376 ]
      //     }
      //   ]
      // }
      console.log(result);
    });
  ```
* function [runInContext](https://bun.com/reference/node/vm/runInContext)(

  code: string,

  contextifiedObject: [Context](https://bun.com/reference/node/vm/Context),

  options?: string | [RunningCodeOptions](https://bun.com/reference/node/vm/RunningCodeOptions)

  ): any;

  The `vm.runInContext()` method compiles `code`, runs it within the context of the `contextifiedObject`, then returns the result. Running code does not have access to the local scope. The `contextifiedObject` object *must* have been previously `contextified` using the createContext method.

  If `options` is a string, then it specifies the filename.

  The following example compiles and executes different scripts using a single `contextified` object:

  ```
  import vm from 'node:vm';

  const contextObject = { globalVar: 1 };
  vm.createContext(contextObject);

  for (let i = 0; i < 10; ++i) {
    vm.runInContext('globalVar *= 2;', contextObject);
  }
  console.log(contextObject);
  // Prints: { globalVar: 1024 }
  ```

  @param code

  The JavaScript code to compile and run.

  @param contextifiedObject

  The `contextified` object that will be used as the `global` when the `code` is compiled and run.

  @returns

  the result of the very last statement executed in the script.
* function [runInNewContext](https://bun.com/reference/node/vm/runInNewContext)(

  code: string,

  contextObject?: number | [Context](https://bun.com/reference/node/vm/Context),

  options?: string | [RunningCodeInNewContextOptions](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions)

  ): any;

  This method is a shortcut to `(new vm.Script(code, options)).runInContext(vm.createContext(options), options)`. If `options` is a string, then it specifies the filename.

  It does several things at once:

  1. Creates a new context.
  2. If `contextObject` is an object, contextifies it with the new context. If `contextObject` is undefined, creates a new object and contextifies it. If `contextObject` is `vm.constants.DONT_CONTEXTIFY`, don't contextify anything.
  3. Compiles the code as a`vm.Script`
  4. Runs the compield code within the created context. The code does not have access to the scope in which this method is called.
  5. Returns the result.

  The following example compiles and executes code that increments a global variable and sets a new one. These globals are contained in the `contextObject`.

  ```
  const vm = require('node:vm');

  const contextObject = {
    animal: 'cat',
    count: 2,
  };

  vm.runInNewContext('count += 1; name = "kitty"', contextObject);
  console.log(contextObject);
  // Prints: { animal: 'cat', count: 3, name: 'kitty' }

  // This would throw if the context is created from a contextified object.
  // vm.constants.DONT_CONTEXTIFY allows creating contexts with ordinary global objects that
  // can be frozen.
  const frozenContext = vm.runInNewContext('Object.freeze(globalThis); globalThis;', vm.constants.DONT_CONTEXTIFY);
  ```

  @param code

  The JavaScript code to compile and run.

  @param contextObject

  Either `vm.constants.DONT_CONTEXTIFY` or an object that will be contextified. If `undefined`, an empty contextified object will be created for backwards compatibility.

  @returns

  the result of the very last statement executed in the script.
* function [runInThisContext](https://bun.com/reference/node/vm/runInThisContext)(

  code: string,

  options?: string | [RunningCodeOptions](https://bun.com/reference/node/vm/RunningCodeOptions)

  ): any;

  `vm.runInThisContext()` compiles `code`, runs it within the context of the current `global` and returns the result. Running code does not have access to local scope, but does have access to the current `global` object.

  If `options` is a string, then it specifies the filename.

  The following example illustrates using both `vm.runInThisContext()` and the JavaScript [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) function to run the same code:

  ```
  import vm from 'node:vm';
  let localVar = 'initial value';

  const vmResult = vm.runInThisContext('localVar = "vm";');
  console.log(`vmResult: '${vmResult}', localVar: '${localVar}'`);
  // Prints: vmResult: 'vm', localVar: 'initial value'

  const evalResult = eval('localVar = "eval";');
  console.log(`evalResult: '${evalResult}', localVar: '${localVar}'`);
  // Prints: evalResult: 'eval', localVar: 'eval'
  ```

  Because `vm.runInThisContext()` does not have access to the local scope, `localVar` is unchanged. In contrast, [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) *does* have access to the local scope, so the value `localVar` is changed. In this way `vm.runInThisContext()` is much like an [indirect `eval()` call](https://es5.github.io/#x10.4.2), e.g.`(0,eval)('code')`.

  ## [Example: Running an HTTP server within a VM](https://bun.com/reference/node/vm#example-running-an-http-server-within-a-vm)

  When using either `script.runInThisContext()` or runInThisContext, the code is executed within the current V8 global context. The code passed to this VM context will have its own isolated scope.

  In order to run a simple web server using the `node:http` module the code passed to the context must either import `node:http` on its own, or have a reference to the `node:http` module passed to it. For instance:

  ```
  'use strict';
  import vm from 'node:vm';

  const code = `
  ((require) => {
  const http = require('node:http');

    http.createServer((request, response) => {
      response.writeHead(200, { 'Content-Type': 'text/plain' });
      response.end('Hello World\\n');
    }).listen(8124);

    console.log('Server running at http://127.0.0.1:8124/');
  })`;

  vm.runInThisContext(code)(require);
  ```

  The `require()` in the above case shares the state with the context it is passed from. This may introduce risks when untrusted code is executed, e.g. altering objects in the context in unwanted ways.

  @param code

  The JavaScript code to compile and run.

  @returns

  the result of the very last statement executed in the script.

## Type definitions

* ### interface [BaseOptions](https://bun.com/reference/node/vm/BaseOptions)

  + [columnOffset](https://bun.com/reference/node/vm/BaseOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [filename](https://bun.com/reference/node/vm/BaseOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [lineOffset](https://bun.com/reference/node/vm/BaseOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
* ### interface [CompileFunctionOptions](https://bun.com/reference/node/vm/CompileFunctionOptions)

  + [cachedData](https://bun.com/reference/node/vm/CompileFunctionOptions/cachedData)?: ArrayBufferView<ArrayBufferLike>

    Provides an optional data with V8's code cache data for the supplied source.
  + [columnOffset](https://bun.com/reference/node/vm/CompileFunctionOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [contextExtensions](https://bun.com/reference/node/vm/CompileFunctionOptions/contextExtensions)?: Object[]

    An array containing a collection of context extensions (objects wrapping the current scope) to be applied while compiling
  + [filename](https://bun.com/reference/node/vm/CompileFunctionOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [importModuleDynamically](https://bun.com/reference/node/vm/CompileFunctionOptions/importModuleDynamically)?: number | [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<Function & Pick<[Script](https://bun.com/reference/node/vm/Script), 'cachedData' | 'cachedDataProduced' | 'cachedDataRejected'>>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [lineOffset](https://bun.com/reference/node/vm/CompileFunctionOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
  + [parsingContext](https://bun.com/reference/node/vm/CompileFunctionOptions/parsingContext)?: [Context](https://bun.com/reference/node/vm/Context)

    The sandbox/context in which the said function should be compiled in.
* ### interface [Context](https://bun.com/reference/node/vm/Context)
* ### interface [CreateContextOptions](https://bun.com/reference/node/vm/CreateContextOptions)

  + [codeGeneration](https://bun.com/reference/node/vm/CreateContextOptions/codeGeneration)?: { strings: boolean; wasm: boolean }
  + [importModuleDynamically](https://bun.com/reference/node/vm/CreateContextOptions/importModuleDynamically)?: number | [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<[Context](https://bun.com/reference/node/vm/Context)>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [microtaskMode](https://bun.com/reference/node/vm/CreateContextOptions/microtaskMode)?: 'afterEvaluate'

    If set to `afterEvaluate`, microtasks will be run immediately after the script has run.
  + [name](https://bun.com/reference/node/vm/CreateContextOptions/name)?: string

    Human-readable name of the newly created context.
  + [origin](https://bun.com/reference/node/vm/CreateContextOptions/origin)?: string

    Corresponds to the newly created context for display purposes. The origin should be formatted like a `URL`, but with only the scheme, host, and port (if necessary), like the value of the `url.origin` property of a URL object. Most notably, this string should omit the trailing slash, as that denotes a path.
* ### interface [MeasureMemoryOptions](https://bun.com/reference/node/vm/MeasureMemoryOptions)

  + [execution](https://bun.com/reference/node/vm/MeasureMemoryOptions/execution)?: 'default' | 'eager'
  + [mode](https://bun.com/reference/node/vm/MeasureMemoryOptions/mode)?: [MeasureMemoryMode](https://bun.com/reference/node/vm/MeasureMemoryMode)
* ### interface [MemoryMeasurement](https://bun.com/reference/node/vm/MemoryMeasurement)

  + [total](https://bun.com/reference/node/vm/MemoryMeasurement/total): { jsMemoryEstimate: number; jsMemoryRange: [number, number] }
* ### interface [ModuleEvaluateOptions](https://bun.com/reference/node/vm/ModuleEvaluateOptions)

  + [breakOnSigint](https://bun.com/reference/node/vm/ModuleEvaluateOptions/breakOnSigint)?: boolean

    If `true`, the execution will be terminated when `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have been attached via `process.on('SIGINT')` will be disabled during script execution, but will continue to work after that. If execution is terminated, an `Error` will be thrown.
  + [timeout](https://bun.com/reference/node/vm/ModuleEvaluateOptions/timeout)?: number

    Specifies the number of milliseconds to execute code before terminating execution. If execution is terminated, an `Error` will be thrown. This value must be a strictly positive integer.
* ### interface [ModuleRequest](https://bun.com/reference/node/vm/ModuleRequest)

  A `ModuleRequest` represents the request to import a module with given import attributes and phase.

  + [attributes](https://bun.com/reference/node/vm/ModuleRequest/attributes): [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes)

    The `"with"` value passed to the `WithClause` in a `ImportDeclaration`, or an empty object if no value was provided.
  + [phase](https://bun.com/reference/node/vm/ModuleRequest/phase): [ImportPhase](https://bun.com/reference/node/module/default/ImportPhase)

    The phase of the requested module (`"source"` or `"evaluation"`).
  + [specifier](https://bun.com/reference/node/vm/ModuleRequest/specifier): string

    The specifier of the requested module.
* ### interface [RunningCodeInNewContextOptions](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions)

  + [breakOnSigint](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/breakOnSigint)?: boolean

    If `true`, the execution will be terminated when `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have been attached via `process.on('SIGINT')` will be disabled during script execution, but will continue to work after that. If execution is terminated, an `Error` will be thrown.
  + [cachedData](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/cachedData)?: ArrayBufferView<ArrayBufferLike>

    Provides an optional data with V8's code cache data for the supplied source.
  + [columnOffset](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [contextCodeGeneration](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/contextCodeGeneration)?: { strings: boolean; wasm: boolean }
  + [contextName](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/contextName)?: string

    Human-readable name of the newly created context.
  + [contextOrigin](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/contextOrigin)?: string

    Origin corresponding to the newly created context for display purposes. The origin should be formatted like a URL, but with only the scheme, host, and port (if necessary), like the value of the `url.origin` property of a `URL` object. Most notably, this string should omit the trailing slash, as that denotes a path.
  + [displayErrors](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/displayErrors)?: boolean

    When `true`, if an `Error` occurs while compiling the `code`, the line of code causing the error is attached to the stack trace.
  + [filename](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [importModuleDynamically](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/importModuleDynamically)?: number | [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<[Script](https://bun.com/reference/node/vm/Script)>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [lineOffset](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
  + [microtaskMode](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/microtaskMode)?: 'afterEvaluate'

    If set to `afterEvaluate`, microtasks will be run immediately after the script has run.
  + [timeout](https://bun.com/reference/node/vm/RunningCodeInNewContextOptions/timeout)?: number

    Specifies the number of milliseconds to execute code before terminating execution. If execution is terminated, an `Error` will be thrown. This value must be a strictly positive integer.
* ### interface [RunningCodeOptions](https://bun.com/reference/node/vm/RunningCodeOptions)

  + [breakOnSigint](https://bun.com/reference/node/vm/RunningCodeOptions/breakOnSigint)?: boolean

    If `true`, the execution will be terminated when `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have been attached via `process.on('SIGINT')` will be disabled during script execution, but will continue to work after that. If execution is terminated, an `Error` will be thrown.
  + [cachedData](https://bun.com/reference/node/vm/RunningCodeOptions/cachedData)?: ArrayBufferView<ArrayBufferLike>

    Provides an optional data with V8's code cache data for the supplied source.
  + [columnOffset](https://bun.com/reference/node/vm/RunningCodeOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [displayErrors](https://bun.com/reference/node/vm/RunningCodeOptions/displayErrors)?: boolean

    When `true`, if an `Error` occurs while compiling the `code`, the line of code causing the error is attached to the stack trace.
  + [filename](https://bun.com/reference/node/vm/RunningCodeOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [importModuleDynamically](https://bun.com/reference/node/vm/RunningCodeOptions/importModuleDynamically)?: number | [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<[Script](https://bun.com/reference/node/vm/Script)>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [lineOffset](https://bun.com/reference/node/vm/RunningCodeOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
  + [timeout](https://bun.com/reference/node/vm/RunningCodeOptions/timeout)?: number

    Specifies the number of milliseconds to execute code before terminating execution. If execution is terminated, an `Error` will be thrown. This value must be a strictly positive integer.
* ### interface [RunningScriptInNewContextOptions](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions)

  + [breakOnSigint](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/breakOnSigint)?: boolean

    If `true`, the execution will be terminated when `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have been attached via `process.on('SIGINT')` will be disabled during script execution, but will continue to work after that. If execution is terminated, an `Error` will be thrown.
  + [columnOffset](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [contextCodeGeneration](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/contextCodeGeneration)?: { strings: boolean; wasm: boolean }
  + [contextName](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/contextName)?: string

    Human-readable name of the newly created context.
  + [contextOrigin](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/contextOrigin)?: string

    Origin corresponding to the newly created context for display purposes. The origin should be formatted like a URL, but with only the scheme, host, and port (if necessary), like the value of the `url.origin` property of a `URL` object. Most notably, this string should omit the trailing slash, as that denotes a path.
  + [displayErrors](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/displayErrors)?: boolean

    When `true`, if an `Error` occurs while compiling the `code`, the line of code causing the error is attached to the stack trace.
  + [filename](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [lineOffset](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
  + [microtaskMode](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/microtaskMode)?: 'afterEvaluate'

    If set to `afterEvaluate`, microtasks will be run immediately after the script has run.
  + [timeout](https://bun.com/reference/node/vm/RunningScriptInNewContextOptions/timeout)?: number

    Specifies the number of milliseconds to execute code before terminating execution. If execution is terminated, an `Error` will be thrown. This value must be a strictly positive integer.
* ### interface [RunningScriptOptions](https://bun.com/reference/node/vm/RunningScriptOptions)

  + [breakOnSigint](https://bun.com/reference/node/vm/RunningScriptOptions/breakOnSigint)?: boolean

    If `true`, the execution will be terminated when `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have been attached via `process.on('SIGINT')` will be disabled during script execution, but will continue to work after that. If execution is terminated, an `Error` will be thrown.
  + [columnOffset](https://bun.com/reference/node/vm/RunningScriptOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [displayErrors](https://bun.com/reference/node/vm/RunningScriptOptions/displayErrors)?: boolean

    When `true`, if an `Error` occurs while compiling the `code`, the line of code causing the error is attached to the stack trace.
  + [filename](https://bun.com/reference/node/vm/RunningScriptOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [lineOffset](https://bun.com/reference/node/vm/RunningScriptOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
  + [timeout](https://bun.com/reference/node/vm/RunningScriptOptions/timeout)?: number

    Specifies the number of milliseconds to execute code before terminating execution. If execution is terminated, an `Error` will be thrown. This value must be a strictly positive integer.
* ### interface [ScriptOptions](https://bun.com/reference/node/vm/ScriptOptions)

  + [cachedData](https://bun.com/reference/node/vm/ScriptOptions/cachedData)?: ArrayBufferView<ArrayBufferLike>

    Provides an optional data with V8's code cache data for the supplied source.
  + [columnOffset](https://bun.com/reference/node/vm/ScriptOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [filename](https://bun.com/reference/node/vm/ScriptOptions/filename)?: string

    Specifies the filename used in stack traces produced by this script.
  + [importModuleDynamically](https://bun.com/reference/node/vm/ScriptOptions/importModuleDynamically)?: number | [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<[Script](https://bun.com/reference/node/vm/Script)>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [lineOffset](https://bun.com/reference/node/vm/ScriptOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
* ### interface [SourceTextModuleOptions](https://bun.com/reference/node/vm/SourceTextModuleOptions)

  + [cachedData](https://bun.com/reference/node/vm/SourceTextModuleOptions/cachedData)?: ArrayBufferView<ArrayBufferLike>

    Provides an optional data with V8's code cache data for the supplied source.
  + [columnOffset](https://bun.com/reference/node/vm/SourceTextModuleOptions/columnOffset)?: number

    Specifies the column number offset that is displayed in stack traces produced by this script.
  + [context](https://bun.com/reference/node/vm/SourceTextModuleOptions/context)?: [Context](https://bun.com/reference/node/vm/Context)
  + [identifier](https://bun.com/reference/node/vm/SourceTextModuleOptions/identifier)?: string

    String used in stack traces.
  + [importModuleDynamically](https://bun.com/reference/node/vm/SourceTextModuleOptions/importModuleDynamically)?: [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<[SourceTextModule](https://bun.com/reference/node/vm/SourceTextModule)>

    Used to specify how the modules should be loaded during the evaluation of this script when `import()` is called. This option is part of the experimental modules API. We do not recommend using it in a production environment. For detailed information, see [Support of dynamic `import()` in compilation APIs](https://nodejs.org/docs/latest-v24.x/api/vm.html#support-of-dynamic-import-in-compilation-apis).
  + [initializeImportMeta](https://bun.com/reference/node/vm/SourceTextModuleOptions/initializeImportMeta)?: (meta: [ImportMeta](https://bun.com/reference/globals/ImportMeta), module: [SourceTextModule](https://bun.com/reference/node/vm/SourceTextModule)) => void

    Called during evaluation of this module to initialize the `import.meta`.
  + [lineOffset](https://bun.com/reference/node/vm/SourceTextModuleOptions/lineOffset)?: number

    Specifies the line number offset that is displayed in stack traces produced by this script.
* ### interface [SyntheticModuleOptions](https://bun.com/reference/node/vm/SyntheticModuleOptions)

  + [context](https://bun.com/reference/node/vm/SyntheticModuleOptions/context)?: [Context](https://bun.com/reference/node/vm/Context)

    The contextified object as returned by the `vm.createContext()` method, to compile and evaluate this module in.
  + [identifier](https://bun.com/reference/node/vm/SyntheticModuleOptions/identifier)?: string

    String used in stack traces.
* type [DynamicModuleLoader](https://bun.com/reference/node/vm/DynamicModuleLoader)<T> = (specifier: string, referrer: T, importAttributes: [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes), phase: [ImportPhase](https://bun.com/reference/node/module/default/ImportPhase)) => [Module](https://bun.com/reference/node/vm/Module) | Promise<[Module](https://bun.com/reference/node/vm/Module)>
* type [MeasureMemoryMode](https://bun.com/reference/node/vm/MeasureMemoryMode) = 'summary' | 'detailed'
* type [ModuleLinker](https://bun.com/reference/node/vm/ModuleLinker) = (specifier: string, referencingModule: [Module](https://bun.com/reference/node/vm/Module), extra: { attributes: [ImportAttributes](https://bun.com/reference/node/module/default/ImportAttributes) }) => [Module](https://bun.com/reference/node/vm/Module) | Promise<[Module](https://bun.com/reference/node/vm/Module)>
* type [ModuleStatus](https://bun.com/reference/node/vm/ModuleStatus) = 'unlinked' | 'linking' | 'linked' | 'evaluating' | 'evaluated' | 'errored'