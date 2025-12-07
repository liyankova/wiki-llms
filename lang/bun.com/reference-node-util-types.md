---
url: https://bun.com/reference/node/util/types
title: Node.js util/types module | API Reference | Bun
source_domain: bun.com
---

# Node.js util/types module | API Reference | Bun

Node.js module

# [util/types](https://bun.com/reference/node/util/types)

The `'node:util/types'` submodule provides type-checking utility functions for Node.js internal and user objects. It includes checks like `isRegExp`, `isDate`, `isBuffer`, and many others.

Use these functions to identify built-in object types accurately in userland code.

* function [isAnyArrayBuffer](https://bun.com/reference/node/util/types/isAnyArrayBuffer)(

  object: unknown

  ): object is ArrayBufferLike;

  Returns `true` if the value is a built-in [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) or [`SharedArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) instance.

  See also `util.types.isArrayBuffer()` and `util.types.isSharedArrayBuffer()`.

  ```
  util.types.isAnyArrayBuffer(new ArrayBuffer());  // Returns true
  util.types.isAnyArrayBuffer(new SharedArrayBuffer());  // Returns true
  ```
* function [isArgumentsObject](https://bun.com/reference/node/util/types/isArgumentsObject)(

  object: unknown

  ): object is IArguments;

  Returns `true` if the value is an `arguments` object.

  ```
  function foo() {
    util.types.isArgumentsObject(arguments);  // Returns true
  }
  ```
* function [isArrayBuffer](https://bun.com/reference/node/util/types/isArrayBuffer)(

  object: unknown

  ): object is [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

  Returns `true` if the value is a built-in [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) instance. This does *not* include [`SharedArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) instances. Usually, it is desirable to test for both; See `util.types.isAnyArrayBuffer()` for that.

  ```
  util.types.isArrayBuffer(new ArrayBuffer());  // Returns true
  util.types.isArrayBuffer(new SharedArrayBuffer());  // Returns false
  ```
* function [isArrayBufferView](https://bun.com/reference/node/util/types/isArrayBufferView)(

  object: unknown

  ): object is ArrayBufferView<ArrayBufferLike>;

  Returns `true` if the value is an instance of one of the [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) views, such as typed array objects or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView). Equivalent to [`ArrayBuffer.isView()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/isView).

  ```
  util.types.isArrayBufferView(new Int8Array());  // true
  util.types.isArrayBufferView(Buffer.from('hello world')); // true
  util.types.isArrayBufferView(new DataView(new ArrayBuffer(16)));  // true
  util.types.isArrayBufferView(new ArrayBuffer());  // false
  ```
* function [isAsyncFunction](https://bun.com/reference/node/util/types/isAsyncFunction)(

  object: unknown

  ): boolean;

  Returns `true` if the value is an [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function). This only reports back what the JavaScript engine is seeing; in particular, the return value may not match the original source code if a transpilation tool was used.

  ```
  util.types.isAsyncFunction(function foo() {});  // Returns false
  util.types.isAsyncFunction(async function foo() {});  // Returns true
  ```
* function [isBigInt64Array](https://bun.com/reference/node/util/types/isBigInt64Array)(

  value: unknown

  ): value is BigInt64Array<ArrayBufferLike>;

  Returns `true` if the value is a `BigInt64Array` instance.

  ```
  util.types.isBigInt64Array(new BigInt64Array());   // Returns true
  util.types.isBigInt64Array(new BigUint64Array());  // Returns false
  ```
* function [isBigIntObject](https://bun.com/reference/node/util/types/isBigIntObject)(

  object: unknown

  ): object is BigInt;

  Returns `true` if the value is a BigInt object, e.g. created by `Object(BigInt(123))`.

  ```
  util.types.isBigIntObject(Object(BigInt(123)));   // Returns true
  util.types.isBigIntObject(BigInt(123));   // Returns false
  util.types.isBigIntObject(123);  // Returns false
  ```
* function [isBigUint64Array](https://bun.com/reference/node/util/types/isBigUint64Array)(

  value: unknown

  ): value is BigUint64Array<ArrayBufferLike>;

  Returns `true` if the value is a `BigUint64Array` instance.

  ```
  util.types.isBigUint64Array(new BigInt64Array());   // Returns false
  util.types.isBigUint64Array(new BigUint64Array());  // Returns true
  ```
* function [isBooleanObject](https://bun.com/reference/node/util/types/isBooleanObject)(

  object: unknown

  ): object is Boolean;

  Returns `true` if the value is a boolean object, e.g. created by `new Boolean()`.

  ```
  util.types.isBooleanObject(false);  // Returns false
  util.types.isBooleanObject(true);   // Returns false
  util.types.isBooleanObject(new Boolean(false)); // Returns true
  util.types.isBooleanObject(new Boolean(true));  // Returns true
  util.types.isBooleanObject(Boolean(false)); // Returns false
  util.types.isBooleanObject(Boolean(true));  // Returns false
  ```
* function [isBoxedPrimitive](https://bun.com/reference/node/util/types/isBoxedPrimitive)(

  object: unknown

  ): object is String | Number | Boolean | Symbol | BigInt;

  Returns `true` if the value is any boxed primitive object, e.g. created by `new Boolean()`, `new String()` or `Object(Symbol())`.

  For example:

  ```
  util.types.isBoxedPrimitive(false); // Returns false
  util.types.isBoxedPrimitive(new Boolean(false)); // Returns true
  util.types.isBoxedPrimitive(Symbol('foo')); // Returns false
  util.types.isBoxedPrimitive(Object(Symbol('foo'))); // Returns true
  util.types.isBoxedPrimitive(Object(BigInt(5))); // Returns true
  ```
* function [isCryptoKey](https://bun.com/reference/node/util/types/isCryptoKey)(

  object: unknown

  ): object is [CryptoKey](https://bun.com/reference/node/crypto/webcrypto/CryptoKey);

  Returns `true` if `value` is a `CryptoKey`, `false` otherwise.
* function [isDataView](https://bun.com/reference/node/util/types/isDataView)(

  object: unknown

  ): object is DataView<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView) instance.

  ```
  const ab = new ArrayBuffer(20);
  util.types.isDataView(new DataView(ab));  // Returns true
  util.types.isDataView(new Float64Array());  // Returns false
  ```

  See also [`ArrayBuffer.isView()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/isView).
* function [isDate](https://bun.com/reference/node/util/types/isDate)(

  object: unknown

  ): object is Date;

  Returns `true` if the value is a built-in [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) instance.

  ```
  util.types.isDate(new Date());  // Returns true
  ```
* function [isExternal](https://bun.com/reference/node/util/types/isExternal)(

  object: unknown

  ): boolean;

  Returns `true` if the value is a native `External` value.

  A native `External` value is a special type of object that contains a raw C++ pointer (`void*`) for access from native code, and has no other properties. Such objects are created either by Node.js internals or native addons. In JavaScript, they are [frozen](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) objects with a `null` prototype.

  ```
  #include <js_native_api.h>
  #include <stdlib.h>
  napi_value result;
  static napi_value MyNapi(napi_env env, napi_callback_info info) {
    int* raw = (int*) malloc(1024);
    napi_status status = napi_create_external(env, (void*) raw, NULL, NULL, &result);
    if (status != napi_ok) {
      napi_throw_error(env, NULL, "napi_create_external failed");
      return NULL;
    }
    return result;
  }
  ...
  DECLARE_NAPI_PROPERTY("myNapi", MyNapi)
  ...
  ```

  ```
  import native from 'napi_addon.node';
  import { types } from 'node:util';

  const data = native.myNapi();
  types.isExternal(data); // returns true
  types.isExternal(0); // returns false
  types.isExternal(new String('foo')); // returns false
  ```

  For further information on `napi_create_external`, refer to [`napi_create_external()`](https://nodejs.org/docs/latest-v24.x/api/n-api.html#napi_create_external).
* function [isFloat16Array](https://bun.com/reference/node/util/types/isFloat16Array)(

  object: unknown

  ): object is Float16Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Float16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float16Array) instance.

  ```
  util.types.isFloat16Array(new ArrayBuffer());  // Returns false
  util.types.isFloat16Array(new Float16Array());  // Returns true
  util.types.isFloat16Array(new Float32Array());  // Returns false
  ```
* function [isFloat32Array](https://bun.com/reference/node/util/types/isFloat32Array)(

  object: unknown

  ): object is Float32Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Float32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array) instance.

  ```
  util.types.isFloat32Array(new ArrayBuffer());  // Returns false
  util.types.isFloat32Array(new Float32Array());  // Returns true
  util.types.isFloat32Array(new Float64Array());  // Returns false
  ```
* function [isFloat64Array](https://bun.com/reference/node/util/types/isFloat64Array)(

  object: unknown

  ): object is Float64Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Float64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array) instance.

  ```
  util.types.isFloat64Array(new ArrayBuffer());  // Returns false
  util.types.isFloat64Array(new Uint8Array());  // Returns false
  util.types.isFloat64Array(new Float64Array());  // Returns true
  ```
* function [isGeneratorFunction](https://bun.com/reference/node/util/types/isGeneratorFunction)(

  object: unknown

  ): object is GeneratorFunction;

  Returns `true` if the value is a generator function. This only reports back what the JavaScript engine is seeing; in particular, the return value may not match the original source code if a transpilation tool was used.

  ```
  util.types.isGeneratorFunction(function foo() {});  // Returns false
  util.types.isGeneratorFunction(function* foo() {});  // Returns true
  ```
* function [isGeneratorObject](https://bun.com/reference/node/util/types/isGeneratorObject)(

  object: unknown

  ): object is Generator<unknown, any, any>;

  Returns `true` if the value is a generator object as returned from a built-in generator function. This only reports back what the JavaScript engine is seeing; in particular, the return value may not match the original source code if a transpilation tool was used.

  ```
  function* foo() {}
  const generator = foo();
  util.types.isGeneratorObject(generator);  // Returns true
  ```
* function [isInt16Array](https://bun.com/reference/node/util/types/isInt16Array)(

  object: unknown

  ): object is Int16Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Int16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array) instance.

  ```
  util.types.isInt16Array(new ArrayBuffer());  // Returns false
  util.types.isInt16Array(new Int16Array());  // Returns true
  util.types.isInt16Array(new Float64Array());  // Returns false
  ```
* function [isInt32Array](https://bun.com/reference/node/util/types/isInt32Array)(

  object: unknown

  ): object is Int32Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Int32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array) instance.

  ```
  util.types.isInt32Array(new ArrayBuffer());  // Returns false
  util.types.isInt32Array(new Int32Array());  // Returns true
  util.types.isInt32Array(new Float64Array());  // Returns false
  ```
* function [isInt8Array](https://bun.com/reference/node/util/types/isInt8Array)(

  object: unknown

  ): object is Int8Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Int8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array) instance.

  ```
  util.types.isInt8Array(new ArrayBuffer());  // Returns false
  util.types.isInt8Array(new Int8Array());  // Returns true
  util.types.isInt8Array(new Float64Array());  // Returns false
  ```
* function [isKeyObject](https://bun.com/reference/node/util/types/isKeyObject)(

  object: unknown

  ): object is [KeyObject](https://bun.com/reference/node/crypto/KeyObject);

  Returns `true` if `value` is a `KeyObject`, `false` otherwise.
* function [isMap](https://bun.com/reference/node/util/types/isMap)<T>(

  object: {} | T

  ): object is T extends ReadonlyMap<any, any> ? unknown extends T<T> ? never : ReadonlyMap<any, any> : Map<unknown, unknown>;

  Returns `true` if the value is a built-in [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) instance.

  ```
  util.types.isMap(new Map());  // Returns true
  ```
* function [isMapIterator](https://bun.com/reference/node/util/types/isMapIterator)(

  object: unknown

  ): boolean;

  Returns `true` if the value is an iterator returned for a built-in [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) instance.

  ```
  const map = new Map();
  util.types.isMapIterator(map.keys());  // Returns true
  util.types.isMapIterator(map.values());  // Returns true
  util.types.isMapIterator(map.entries());  // Returns true
  util.types.isMapIterator(map[Symbol.iterator]());  // Returns true
  ```
* function [isModuleNamespaceObject](https://bun.com/reference/node/util/types/isModuleNamespaceObject)(

  value: unknown

  ): boolean;

  Returns `true` if the value is an instance of a [Module Namespace Object](https://tc39.github.io/ecma262/#sec-module-namespace-exotic-objects).

  ```
  import * as ns from './a.js';

  util.types.isModuleNamespaceObject(ns);  // Returns true
  ```
* function [isNumberObject](https://bun.com/reference/node/util/types/isNumberObject)(

  object: unknown

  ): object is Number;

  Returns `true` if the value is a number object, e.g. created by `new Number()`.

  ```
  util.types.isNumberObject(0);  // Returns false
  util.types.isNumberObject(new Number(0));   // Returns true
  ```
* function [isPromise](https://bun.com/reference/node/util/types/isPromise)(

  object: unknown

  ): object is Promise<unknown>;

  Returns `true` if the value is a built-in [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

  ```
  util.types.isPromise(Promise.resolve(42));  // Returns true
  ```
* function [isProxy](https://bun.com/reference/node/util/types/isProxy)(

  object: unknown

  ): boolean;

  Returns `true` if the value is a [`Proxy`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) instance.

  ```
  const target = {};
  const proxy = new Proxy(target, {});
  util.types.isProxy(target);  // Returns false
  util.types.isProxy(proxy);  // Returns true
  ```
* function [isRegExp](https://bun.com/reference/node/util/types/isRegExp)(

  object: unknown

  ): object is RegExp;

  Returns `true` if the value is a regular expression object.

  ```
  util.types.isRegExp(/abc/);  // Returns true
  util.types.isRegExp(new RegExp('abc'));  // Returns true
  ```
* function [isSet](https://bun.com/reference/node/util/types/isSet)<T>(

  object: {} | T

  ): object is T extends ReadonlySet<any> ? unknown extends T<T> ? never : ReadonlySet<any> : Set<unknown>;

  Returns `true` if the value is a built-in [`Set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) instance.

  ```
  util.types.isSet(new Set());  // Returns true
  ```
* function [isSetIterator](https://bun.com/reference/node/util/types/isSetIterator)(

  object: unknown

  ): boolean;

  Returns `true` if the value is an iterator returned for a built-in [`Set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) instance.

  ```
  const set = new Set();
  util.types.isSetIterator(set.keys());  // Returns true
  util.types.isSetIterator(set.values());  // Returns true
  util.types.isSetIterator(set.entries());  // Returns true
  util.types.isSetIterator(set[Symbol.iterator]());  // Returns true
  ```
* function [isSharedArrayBuffer](https://bun.com/reference/node/util/types/isSharedArrayBuffer)(

  object: unknown

  ): object is [SharedArrayBuffer](https://bun.com/reference/globals/SharedArrayBuffer);

  Returns `true` if the value is a built-in [`SharedArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) instance. This does *not* include [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) instances. Usually, it is desirable to test for both; See `util.types.isAnyArrayBuffer()` for that.

  ```
  util.types.isSharedArrayBuffer(new ArrayBuffer());  // Returns false
  util.types.isSharedArrayBuffer(new SharedArrayBuffer());  // Returns true
  ```
* function [isStringObject](https://bun.com/reference/node/util/types/isStringObject)(

  object: unknown

  ): object is String;

  Returns `true` if the value is a string object, e.g. created by `new String()`.

  ```
  util.types.isStringObject('foo');  // Returns false
  util.types.isStringObject(new String('foo'));   // Returns true
  ```
* function [isSymbolObject](https://bun.com/reference/node/util/types/isSymbolObject)(

  object: unknown

  ): object is Symbol;

  Returns `true` if the value is a symbol object, created by calling `Object()` on a `Symbol` primitive.

  ```
  const symbol = Symbol('foo');
  util.types.isSymbolObject(symbol);  // Returns false
  util.types.isSymbolObject(Object(symbol));   // Returns true
  ```
* function [isTypedArray](https://bun.com/reference/node/util/types/isTypedArray)(

  object: unknown

  ): object is TypedArray<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) instance.

  ```
  util.types.isTypedArray(new ArrayBuffer());  // Returns false
  util.types.isTypedArray(new Uint8Array());  // Returns true
  util.types.isTypedArray(new Float64Array());  // Returns true
  ```

  See also [`ArrayBuffer.isView()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/isView).
* function [isUint16Array](https://bun.com/reference/node/util/types/isUint16Array)(

  object: unknown

  ): object is Uint16Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Uint16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array) instance.

  ```
  util.types.isUint16Array(new ArrayBuffer());  // Returns false
  util.types.isUint16Array(new Uint16Array());  // Returns true
  util.types.isUint16Array(new Float64Array());  // Returns false
  ```
* function [isUint32Array](https://bun.com/reference/node/util/types/isUint32Array)(

  object: unknown

  ): object is Uint32Array<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Uint32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array) instance.

  ```
  util.types.isUint32Array(new ArrayBuffer());  // Returns false
  util.types.isUint32Array(new Uint32Array());  // Returns true
  util.types.isUint32Array(new Float64Array());  // Returns false
  ```
* function [isUint8Array](https://bun.com/reference/node/util/types/isUint8Array)(

  object: unknown

  ): object is [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) instance.

  ```
  util.types.isUint8Array(new ArrayBuffer());  // Returns false
  util.types.isUint8Array(new Uint8Array());  // Returns true
  util.types.isUint8Array(new Float64Array());  // Returns false
  ```
* function [isUint8ClampedArray](https://bun.com/reference/node/util/types/isUint8ClampedArray)(

  object: unknown

  ): object is Uint8ClampedArray<ArrayBufferLike>;

  Returns `true` if the value is a built-in [`Uint8ClampedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray) instance.

  ```
  util.types.isUint8ClampedArray(new ArrayBuffer());  // Returns false
  util.types.isUint8ClampedArray(new Uint8ClampedArray());  // Returns true
  util.types.isUint8ClampedArray(new Float64Array());  // Returns false
  ```
* function [isWeakMap](https://bun.com/reference/node/util/types/isWeakMap)(

  object: unknown

  ): object is WeakMap<object, unknown>;

  Returns `true` if the value is a built-in [`WeakMap`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap) instance.

  ```
  util.types.isWeakMap(new WeakMap());  // Returns true
  ```
* function [isWeakSet](https://bun.com/reference/node/util/types/isWeakSet)(

  object: unknown

  ): object is WeakSet<object>;

  Returns `true` if the value is a built-in [`WeakSet`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet) instance.

  ```
  util.types.isWeakSet(new WeakSet());  // Returns true
  ```