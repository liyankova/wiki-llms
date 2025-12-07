---
url: https://bun.com/reference/node/util
title: Node.js util module | API Reference | Bun
source_domain: bun.com
---

# Node.js util module | API Reference | Bun

Node.js module

# [util](https://bun.com/reference/node/util)

The `'node:util'` module provides utility functions for debugging and supporting internal Node.js operations. It includes `util.format`, `util.callbackify`, `util.promisify`, and `util.inspect`.

These helpers simplify error handling, convert callbacks to promises, format strings, and inspect objects with configurable depth and styling.

Works in Bun

Most utility functions are implemented. Missing specific functions related to call sites, system errors, and transferable AbortSignals/Controllers.

* function [inspect](https://bun.com/reference/node/util/inspect)(

  object: any,

  showHidden?: boolean,

  depth?: null | number,

  color?: boolean

  ): string;

  The `util.inspect()` method returns a string representation of `object` that is intended for debugging. The output of `util.inspect` may change at any time and should not be depended upon programmatically. Additional `options` may be passed that alter the result. `util.inspect()` will use the constructor's name and/or `Symbol.toStringTag` property to make an identifiable tag for an inspected value.

  ```
  class Foo {
    get [Symbol.toStringTag]() {
      return 'bar';
    }
  }

  class Bar {}

  const baz = Object.create(null, { [Symbol.toStringTag]: { value: 'foo' } });

  util.inspect(new Foo()); // 'Foo [bar] {}'
  util.inspect(new Bar()); // 'Bar {}'
  util.inspect(baz);       // '[foo] {}'
  ```

  Circular references point to their anchor by using a reference index:

  ```
  import { inspect } from 'node:util';

  const obj = {};
  obj.a = [obj];
  obj.b = {};
  obj.b.inner = obj.b;
  obj.b.obj = obj;

  console.log(inspect(obj));
  // <ref *1> {
  //   a: [ [Circular *1] ],
  //   b: <ref *2> { inner: [Circular *2], obj: [Circular *1] }
  // }
  ```

  The following example inspects all properties of the `util` object:

  ```
  import util from 'node:util';

  console.log(util.inspect(util, { showHidden: true, depth: null }));
  ```

  The following example highlights the effect of the `compact` option:

  ```
  import { inspect } from 'node:util';

  const o = {
    a: [1, 2, [[
      'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit, sed do ' +
        'eiusmod \ntempor incididunt ut labore et dolore magna aliqua.',
      'test',
      'foo']], 4],
    b: new Map([['za', 1], ['zb', 'test']]),
  };
  console.log(inspect(o, { compact: true, depth: 5, breakLength: 80 }));

  // { a:
  //   [ 1,
  //     2,
  //     [ [ 'Lorem ipsum dolor sit amet,\nconsectetur [...]', // A long line
  //           'test',
  //           'foo' ] ],
  //     4 ],
  //   b: Map(2) { 'za' => 1, 'zb' => 'test' } }

  // Setting `compact` to false or an integer creates more reader friendly output.
  console.log(inspect(o, { compact: false, depth: 5, breakLength: 80 }));

  // {
  //   a: [
  //     1,
  //     2,
  //     [
  //       [
  //         'Lorem ipsum dolor sit amet,\n' +
  //           'consectetur adipiscing elit, sed do eiusmod \n' +
  //           'tempor incididunt ut labore et dolore magna aliqua.',
  //         'test',
  //         'foo'
  //       ]
  //     ],
  //     4
  //   ],
  //   b: Map(2) {
  //     'za' => 1,
  //     'zb' => 'test'
  //   }
  // }

  // Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
  // single line.
  ```

  The `showHidden` option allows `WeakMap` and `WeakSet` entries to be inspected. If there are more entries than `maxArrayLength`, there is no guarantee which entries are displayed. That means retrieving the same `WeakSet` entries twice may result in different output. Furthermore, entries with no remaining strong references may be garbage collected at any time.

  ```
  import { inspect } from 'node:util';

  const obj = { a: 1 };
  const obj2 = { b: 2 };
  const weakSet = new WeakSet([obj, obj2]);

  console.log(inspect(weakSet, { showHidden: true }));
  // WeakSet { { a: 1 }, { b: 2 } }
  ```

  The `sorted` option ensures that an object's property insertion order does not impact the result of `util.inspect()`.

  ```
  import { inspect } from 'node:util';
  import assert from 'node:assert';

  const o1 = {
    b: [2, 3, 1],
    a: '`a` comes before `b`',
    c: new Set([2, 3, 1]),
  };
  console.log(inspect(o1, { sorted: true }));
  // { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set(3) { 1, 2, 3 } }
  console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
  // { c: Set(3) { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

  const o2 = {
    c: new Set([2, 1, 3]),
    a: '`a` comes before `b`',
    b: [2, 3, 1],
  };
  assert.strict.equal(
    inspect(o1, { sorted: true }),
    inspect(o2, { sorted: true }),
  );
  ```

  The `numericSeparator` option adds an underscore every three digits to all numbers.

  ```
  import { inspect } from 'node:util';

  const thousand = 1000;
  const million = 1000000;
  const bigNumber = 123456789n;
  const bigDecimal = 1234.12345;

  console.log(inspect(thousand, { numericSeparator: true }));
  // 1_000
  console.log(inspect(million, { numericSeparator: true }));
  // 1_000_000
  console.log(inspect(bigNumber, { numericSeparator: true }));
  // 123_456_789n
  console.log(inspect(bigDecimal, { numericSeparator: true }));
  // 1_234.123_45
  ```

  `util.inspect()` is a synchronous method intended for debugging. Its maximum output length is approximately 128 MiB. Inputs that result in longer output will be truncated.

  @param object

  Any JavaScript primitive or `Object`.

  @returns

  The representation of `object`.

  function [inspect](https://bun.com/reference/node/util/inspect)(

  object: any,

  options?: [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

  ): string;

  The `util.inspect()` method returns a string representation of `object` that is intended for debugging. The output of `util.inspect` may change at any time and should not be depended upon programmatically. Additional `options` may be passed that alter the result. `util.inspect()` will use the constructor's name and/or `Symbol.toStringTag` property to make an identifiable tag for an inspected value.

  ```
  class Foo {
    get [Symbol.toStringTag]() {
      return 'bar';
    }
  }

  class Bar {}

  const baz = Object.create(null, { [Symbol.toStringTag]: { value: 'foo' } });

  util.inspect(new Foo()); // 'Foo [bar] {}'
  util.inspect(new Bar()); // 'Bar {}'
  util.inspect(baz);       // '[foo] {}'
  ```

  Circular references point to their anchor by using a reference index:

  ```
  import { inspect } from 'node:util';

  const obj = {};
  obj.a = [obj];
  obj.b = {};
  obj.b.inner = obj.b;
  obj.b.obj = obj;

  console.log(inspect(obj));
  // <ref *1> {
  //   a: [ [Circular *1] ],
  //   b: <ref *2> { inner: [Circular *2], obj: [Circular *1] }
  // }
  ```

  The following example inspects all properties of the `util` object:

  ```
  import util from 'node:util';

  console.log(util.inspect(util, { showHidden: true, depth: null }));
  ```

  The following example highlights the effect of the `compact` option:

  ```
  import { inspect } from 'node:util';

  const o = {
    a: [1, 2, [[
      'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit, sed do ' +
        'eiusmod \ntempor incididunt ut labore et dolore magna aliqua.',
      'test',
      'foo']], 4],
    b: new Map([['za', 1], ['zb', 'test']]),
  };
  console.log(inspect(o, { compact: true, depth: 5, breakLength: 80 }));

  // { a:
  //   [ 1,
  //     2,
  //     [ [ 'Lorem ipsum dolor sit amet,\nconsectetur [...]', // A long line
  //           'test',
  //           'foo' ] ],
  //     4 ],
  //   b: Map(2) { 'za' => 1, 'zb' => 'test' } }

  // Setting `compact` to false or an integer creates more reader friendly output.
  console.log(inspect(o, { compact: false, depth: 5, breakLength: 80 }));

  // {
  //   a: [
  //     1,
  //     2,
  //     [
  //       [
  //         'Lorem ipsum dolor sit amet,\n' +
  //           'consectetur adipiscing elit, sed do eiusmod \n' +
  //           'tempor incididunt ut labore et dolore magna aliqua.',
  //         'test',
  //         'foo'
  //       ]
  //     ],
  //     4
  //   ],
  //   b: Map(2) {
  //     'za' => 1,
  //     'zb' => 'test'
  //   }
  // }

  // Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
  // single line.
  ```

  The `showHidden` option allows `WeakMap` and `WeakSet` entries to be inspected. If there are more entries than `maxArrayLength`, there is no guarantee which entries are displayed. That means retrieving the same `WeakSet` entries twice may result in different output. Furthermore, entries with no remaining strong references may be garbage collected at any time.

  ```
  import { inspect } from 'node:util';

  const obj = { a: 1 };
  const obj2 = { b: 2 };
  const weakSet = new WeakSet([obj, obj2]);

  console.log(inspect(weakSet, { showHidden: true }));
  // WeakSet { { a: 1 }, { b: 2 } }
  ```

  The `sorted` option ensures that an object's property insertion order does not impact the result of `util.inspect()`.

  ```
  import { inspect } from 'node:util';
  import assert from 'node:assert';

  const o1 = {
    b: [2, 3, 1],
    a: '`a` comes before `b`',
    c: new Set([2, 3, 1]),
  };
  console.log(inspect(o1, { sorted: true }));
  // { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set(3) { 1, 2, 3 } }
  console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
  // { c: Set(3) { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

  const o2 = {
    c: new Set([2, 1, 3]),
    a: '`a` comes before `b`',
    b: [2, 3, 1],
  };
  assert.strict.equal(
    inspect(o1, { sorted: true }),
    inspect(o2, { sorted: true }),
  );
  ```

  The `numericSeparator` option adds an underscore every three digits to all numbers.

  ```
  import { inspect } from 'node:util';

  const thousand = 1000;
  const million = 1000000;
  const bigNumber = 123456789n;
  const bigDecimal = 1234.12345;

  console.log(inspect(thousand, { numericSeparator: true }));
  // 1_000
  console.log(inspect(million, { numericSeparator: true }));
  // 1_000_000
  console.log(inspect(bigNumber, { numericSeparator: true }));
  // 123_456_789n
  console.log(inspect(bigDecimal, { numericSeparator: true }));
  // 1_234.123_45
  ```

  `util.inspect()` is a synchronous method intended for debugging. Its maximum output length is approximately 128 MiB. Inputs that result in longer output will be truncated.

  @param object

  Any JavaScript primitive or `Object`.

  @returns

  The representation of `object`.

  ### namespace [inspect](https://bun.com/reference/node/util/inspect)

  + const [colors](https://bun.com/reference/node/util/inspect/colors): NodeJS.Dict<[number, number]>
  + const [custom](https://bun.com/reference/node/util/inspect/custom): unique symbol

    That can be used to declare custom inspect functions.
  + const [defaultOptions](https://bun.com/reference/node/util/inspect/defaultOptions): [InspectOptions](https://bun.com/reference/node/util/InspectOptions)
  + const [replDefaults](https://bun.com/reference/node/util/inspect/replDefaults): [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

    Allows changing inspect settings from the repl.
  + const [styles](https://bun.com/reference/node/util/inspect/styles): { [K in [Style](https://bun.com/reference/node/util/Style)]: string }
* function [promisify](https://bun.com/reference/node/util/promisify)<TCustom extends Function>(

  fn: [CustomPromisify](https://bun.com/reference/node/util/CustomPromisify)<TCustom>

  ): TCustom;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<TResult>(

  fn: (callback: (err: any, result: TResult) => void) => void

  ): () => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)(

  fn: (callback: (err?: any) => void) => void

  ): () => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, TResult>(

  fn: (arg1: T1, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1>(

  fn: (arg1: T1, callback: (err?: any) => void) => void

  ): (arg1: T1) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, TResult>(

  fn: (arg1: T1, arg2: T2, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2>(

  fn: (arg1: T1, arg2: T2, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3>(

  fn: (arg1: T1, arg2: T2, arg3: T3, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, T5, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, T5>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)(

  fn: Function

  ): Function;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  ### namespace [promisify](https://bun.com/reference/node/util/promisify)

  + const [custom](https://bun.com/reference/node/util/promisify/custom): unique symbol

    That can be used to declare custom promisified variants of functions.
* ### class [MIMEParams](https://bun.com/reference/node/util/MIMEParams)

  The `MIMEParams` API provides read and write access to the parameters of a `MIMEType`.

  + [[Symbol.iterator]](https://bun.com/reference/node/util/MIMEParams/[iterator])(): Iterator<[name: string, value: string]>;

    Returns an iterator over each of the name-value pairs in the parameters.
  + [delete](https://bun.com/reference/node/util/MIMEParams/delete)(

    name: string

    ): void;

    Remove all name-value pairs whose name is `name`.
  + [entries](https://bun.com/reference/node/util/MIMEParams/entries)(): Iterator<[name: string, value: string]>;

    Returns an iterator over each of the name-value pairs in the parameters. Each item of the iterator is a JavaScript `Array`. The first item of the array is the `name`, the second item of the array is the `value`.
  + [get](https://bun.com/reference/node/util/MIMEParams/get)(

    name: string

    ): null | string;

    Returns the value of the first name-value pair whose name is `name`. If there are no such pairs, `null` is returned.

    @returns

    or `null` if there is no name-value pair with the given `name`.
  + [has](https://bun.com/reference/node/util/MIMEParams/has)(

    name: string

    ): boolean;

    Returns `true` if there is at least one name-value pair whose name is `name`.
  + [keys](https://bun.com/reference/node/util/MIMEParams/keys)(): Iterator<string>;

    Returns an iterator over the names of each name-value pair.

    ```
    import { MIMEType } from 'node:util';

    const { params } = new MIMEType('text/plain;foo=0;bar=1');
    for (const name of params.keys()) {
      console.log(name);
    }
    // Prints:
    //   foo
    //   bar
    ```
  + [set](https://bun.com/reference/node/util/MIMEParams/set)(

    name: string,

    value: string

    ): void;

    Sets the value in the `MIMEParams` object associated with `name` to `value`. If there are any pre-existing name-value pairs whose names are `name`, set the first such pair's value to `value`.

    ```
    import { MIMEType } from 'node:util';

    const { params } = new MIMEType('text/plain;foo=0;bar=1');
    params.set('foo', 'def');
    params.set('baz', 'xyz');
    console.log(params.toString());
    // Prints: foo=def;bar=1;baz=xyz
    ```
  + [values](https://bun.com/reference/node/util/MIMEParams/values)(): Iterator<string>;

    Returns an iterator over the values of each name-value pair.
* ### class [MIMEType](https://bun.com/reference/node/util/MIMEType)

  An implementation of [the MIMEType class](https://bmeck.github.io/node-proposal-mime-api/).

  In accordance with browser conventions, all properties of `MIMEType` objects are implemented as getters and setters on the class prototype, rather than as data properties on the object itself.

  A MIME string is a structured string containing multiple meaningful components. When parsed, a `MIMEType` object is returned containing properties for each of these components.

  + readonly [essence](https://bun.com/reference/node/util/MIMEType/essence): string

    Gets the essence of the MIME. This property is read only. Use `mime.type` or `mime.subtype` to alter the MIME.

    ```
    import { MIMEType } from 'node:util';

    const myMIME = new MIMEType('text/javascript;key=value');
    console.log(myMIME.essence);
    // Prints: text/javascript
    myMIME.type = 'application';
    console.log(myMIME.essence);
    // Prints: application/javascript
    console.log(String(myMIME));
    // Prints: application/javascript;key=value
    ```
  + readonly [params](https://bun.com/reference/node/util/MIMEType/params): [MIMEParams](https://bun.com/reference/node/util/MIMEParams)

    Gets the `MIMEParams` object representing the parameters of the MIME. This property is read-only. See `MIMEParams` documentation for details.
  + [subtype](https://bun.com/reference/node/util/MIMEType/subtype): string

    Gets and sets the subtype portion of the MIME.

    ```
    import { MIMEType } from 'node:util';

    const myMIME = new MIMEType('text/ecmascript');
    console.log(myMIME.subtype);
    // Prints: ecmascript
    myMIME.subtype = 'javascript';
    console.log(myMIME.subtype);
    // Prints: javascript
    console.log(String(myMIME));
    // Prints: text/javascript
    ```
  + [type](https://bun.com/reference/node/util/MIMEType/type): string

    Gets and sets the type portion of the MIME.

    ```
    import { MIMEType } from 'node:util';

    const myMIME = new MIMEType('text/javascript');
    console.log(myMIME.type);
    // Prints: text
    myMIME.type = 'application';
    console.log(myMIME.type);
    // Prints: application
    console.log(String(myMIME));
    // Prints: application/javascript
    ```
  + [toString](https://bun.com/reference/node/util/MIMEType/toString)(): string;

    The `toString()` method on the `MIMEType` object returns the serialized MIME.

    Because of the need for standard compliance, this method does not allow users to customize the serialization process of the MIME.
* ### class [TextDecoder](https://bun.com/reference/node/util/TextDecoder)

  An implementation of the [WHATWG Encoding Standard](https://encoding.spec.whatwg.org/) `TextDecoder` API.

  ```
  const decoder = new TextDecoder();
  const u8arr = new Uint8Array([72, 101, 108, 108, 111]);
  console.log(decoder.decode(u8arr)); // Hello
  ```

  + readonly [encoding](https://bun.com/reference/node/util/TextDecoder/encoding): string

    The encoding supported by the `TextDecoder` instance.
  + readonly [fatal](https://bun.com/reference/node/util/TextDecoder/fatal): boolean

    The value will be `true` if decoding errors result in a `TypeError` being thrown.
  + readonly [ignoreBOM](https://bun.com/reference/node/util/TextDecoder/ignoreBOM): boolean

    The value will be `true` if the decoding result will include the byte order mark.
  + [decode](https://bun.com/reference/node/util/TextDecoder/decode)(

    input?: null | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | ArrayBufferView<ArrayBufferLike>,

    options?: { stream: boolean }

    ): string;

    Decodes the `input` and returns a string. If `options.stream` is `true`, any incomplete byte sequences occurring at the end of the `input` are buffered internally and emitted after the next call to `textDecoder.decode()`.

    If `textDecoder.fatal` is `true`, decoding errors that occur will result in a `TypeError` being thrown.

    @param input

    An `ArrayBuffer`, `DataView`, or `TypedArray` instance containing the encoded data.
* ### class [TextEncoder](https://bun.com/reference/node/util/TextEncoder)

  An implementation of the [WHATWG Encoding Standard](https://encoding.spec.whatwg.org/) `TextEncoder` API. All instances of `TextEncoder` only support UTF-8 encoding.

  ```
  const encoder = new TextEncoder();
  const uint8array = encoder.encode('this is some data');
  ```

  The `TextEncoder` class is also available on the global object.

  + readonly [encoding](https://bun.com/reference/node/util/TextEncoder/encoding): string

    The encoding supported by the `TextEncoder` instance. Always set to `'utf-8'`.
  + [encode](https://bun.com/reference/node/util/TextEncoder/encode)(

    input?: string

    ): NonSharedUint8Array;

    UTF-8 encodes the `input` string and returns a `Uint8Array` containing the encoded bytes.

    @param input

    The text to encode.
  + [encodeInto](https://bun.com/reference/node/util/TextEncoder/encodeInto)(

    src: string,

    dest: [Uint8Array](https://bun.com/reference/globals/Uint8Array)

    ): [EncodeIntoResult](https://bun.com/reference/node/util/EncodeIntoResult);

    UTF-8 encodes the `src` string to the `dest` Uint8Array and returns an object containing the read Unicode code units and written UTF-8 bytes.

    ```
    const encoder = new TextEncoder();
    const src = 'this is some data';
    const dest = new Uint8Array(10);
    const { read, written } = encoder.encodeInto(src, dest);
    ```

    @param src

    The text to encode.

    @param dest

    The array to hold the encode result.
* function [aborted](https://bun.com/reference/node/util/aborted)(

  signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

  resource: any

  ): Promise<void>;

  Listens to abort event on the provided `signal` and returns a promise that resolves when the `signal` is aborted. If `resource` is provided, it weakly references the operation's associated object, so if `resource` is garbage collected before the `signal` aborts, then returned promise shall remain pending. This prevents memory leaks in long-running or non-cancelable operations.

  ```
  import { aborted } from 'node:util';

  // Obtain an object with an abortable signal, like a custom resource or operation.
  const dependent = obtainSomethingAbortable();

  // Pass `dependent` as the resource, indicating the promise should only resolve
  // if `dependent` is still in memory when the signal is aborted.
  aborted(dependent.signal, dependent).then(() => {
    // This code runs when `dependent` is aborted.
    console.log('Dependent resource was aborted.');
  });

  // Simulate an event that triggers the abort.
  dependent.on('event', () => {
    dependent.abort(); // This will cause the `aborted` promise to resolve.
  });
  ```

  @param resource

  Any non-null object tied to the abortable operation and held weakly. If `resource` is garbage collected before the `signal` aborts, the promise remains pending, allowing Node.js to stop tracking it. This helps prevent memory leaks in long-running or non-cancelable operations.
* function [callbackify](https://bun.com/reference/node/util/callbackify)(

  fn: () => Promise<void>

  ): (callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<TResult>(

  fn: () => Promise<TResult>

  ): (callback: (err: ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1>(

  fn: (arg1: T1) => Promise<void>

  ): (arg1: T1, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, TResult>(

  fn: (arg1: T1) => Promise<TResult>

  ): (arg1: T1, callback: (err: ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2>(

  fn: (arg1: T1, arg2: T2) => Promise<void>

  ): (arg1: T1, arg2: T2, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, TResult>(

  fn: (arg1: T1, arg2: T2) => Promise<TResult>

  ): (arg1: T1, arg2: T2, callback: (err: null | ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3>(

  fn: (arg1: T1, arg2: T2, arg3: T3) => Promise<void>

  ): (arg1: T1, arg2: T2, arg3: T3, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3) => Promise<TResult>

  ): (arg1: T1, arg2: T2, arg3: T3, callback: (err: null | ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<void>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<TResult>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err: null | ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4, T5>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<void>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4, T5, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<TResult>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err: null | ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4, T5, T6>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, arg6: T6) => Promise<void>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, arg6: T6, callback: (err: ErrnoException) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function

  function [callbackify](https://bun.com/reference/node/util/callbackify)<T1, T2, T3, T4, T5, T6, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, arg6: T6) => Promise<TResult>

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, arg6: T6, callback: (err: null | ErrnoException, result: TResult) => void) => void;

  Takes an `async` function (or a function that returns a `Promise`) and returns a function following the error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument. In the callback, the first argument will be the rejection reason (or `null` if the `Promise` resolved), and the second argument will be the resolved value.

  ```
  import { callbackify } from 'node:util';

  async function fn() {
    return 'hello world';
  }
  const callbackFunction = callbackify(fn);

  callbackFunction((err, ret) => {
    if (err) throw err;
    console.log(ret);
  });
  ```

  Will print:

  ```
  hello world
  ```

  The callback is executed asynchronously, and will have a limited stack trace. If the callback throws, the process will emit an `'uncaughtException'` event, and if not handled will exit.

  Since `null` has a special meaning as the first argument to a callback, if a wrapped function rejects a `Promise` with a falsy value as a reason, the value is wrapped in an `Error` with the original value stored in a field named `reason`.

  ```
  function fn() {
    return Promise.reject(null);
  }
  const callbackFunction = util.callbackify(fn);

  callbackFunction((err, ret) => {
    // When the Promise was rejected with `null` it is wrapped with an Error and
    // the original value is stored in `reason`.
    err && Object.hasOwn(err, 'reason') && err.reason === null;  // true
  });
  ```

  @param fn

  An `async` function

  @returns

  a callback style function
* function [debuglog](https://bun.com/reference/node/util/debuglog)(

  section: string,

  callback?: (fn: [DebugLoggerFunction](https://bun.com/reference/node/util/DebugLoggerFunction)) => void

  ): [DebugLogger](https://bun.com/reference/node/util/DebugLogger);

  The `util.debuglog()` method is used to create a function that conditionally writes debug messages to `stderr` based on the existence of the `NODE_DEBUG` environment variable. If the `section` name appears within the value of that environment variable, then the returned function operates similar to `console.error()`. If not, then the returned function is a no-op.

  ```
  import { debuglog } from 'node:util';
  const log = debuglog('foo');

  log('hello from foo [%d]', 123);
  ```

  If this program is run with `NODE_DEBUG=foo` in the environment, then it will output something like:

  ```
  FOO 3245: hello from foo [123]
  ```

  where `3245` is the process id. If it is not run with that environment variable set, then it will not print anything.

  The `section` supports wildcard also:

  ```
  import { debuglog } from 'node:util';
  const log = debuglog('foo');

  log('hi there, it\'s foo-bar [%d]', 2333);
  ```

  if it is run with `NODE_DEBUG=foo*` in the environment, then it will output something like:

  ```
  FOO-BAR 3257: hi there, it's foo-bar [2333]
  ```

  Multiple comma-separated `section` names may be specified in the `NODE_DEBUG` environment variable: `NODE_DEBUG=fs,net,tls`.

  The optional `callback` argument can be used to replace the logging function with a different function that doesn't have any initialization or unnecessary wrapping.

  ```
  import { debuglog } from 'node:util';
  let log = debuglog('internals', (debug) => {
    // Replace with a logging function that optimizes out
    // testing if the section is enabled
    log = debug;
  });
  ```

  @param section

  A string identifying the portion of the application for which the `debuglog` function is being created.

  @param callback

  A callback invoked the first time the logging function is called with a function argument that is a more optimized logging function.

  @returns

  The logging function
* function [diff](https://bun.com/reference/node/util/diff)(

  actual: string | readonly string[],

  expected: string | readonly string[]

  ): [DiffEntry](https://bun.com/reference/node/util/DiffEntry)[];

  `util.diff()` compares two string or array values and returns an array of difference entries. It uses the Myers diff algorithm to compute minimal differences, which is the same algorithm used internally by assertion error messages.

  If the values are equal, an empty array is returned.

  ```
  const { diff } = require('node:util');

  // Comparing strings
  const actualString = '12345678';
  const expectedString = '12!!5!7!';
  console.log(diff(actualString, expectedString));
  // [
  //   [0, '1'],
  //   [0, '2'],
  //   [1, '3'],
  //   [1, '4'],
  //   [-1, '!'],
  //   [-1, '!'],
  //   [0, '5'],
  //   [1, '6'],
  //   [-1, '!'],
  //   [0, '7'],
  //   [1, '8'],
  //   [-1, '!'],
  // ]
  // Comparing arrays
  const actualArray = ['1', '2', '3'];
  const expectedArray = ['1', '3', '4'];
  console.log(diff(actualArray, expectedArray));
  // [
  //   [0, '1'],
  //   [1, '2'],
  //   [0, '3'],
  //   [-1, '4'],
  // ]
  // Equal values return empty array
  console.log(diff('same', 'same'));
  // []
  ```

  @param actual

  The first value to compare

  @param expected

  The second value to compare

  @returns

  An array of difference entries. Each entry is an array with two elements:

  + Index 0: `number` Operation code: `-1` for delete, `0` for no-op/unchanged, `1` for insert
  + Index 1: `string` The value associated with the operation
* function [format](https://bun.com/reference/node/util/format)(

  format?: any,

  ...param: any[]

  ): string;

  The `util.format()` method returns a formatted string using the first argument as a `printf`-like format string which can contain zero or more format specifiers. Each specifier is replaced with the converted value from the corresponding argument. Supported specifiers are:

  If a specifier does not have a corresponding argument, it is not replaced:

  ```
  util.format('%s:%s', 'foo');
  // Returns: 'foo:%s'
  ```

  Values that are not part of the format string are formatted using `util.inspect()` if their type is not `string`.

  If there are more arguments passed to the `util.format()` method than the number of specifiers, the extra arguments are concatenated to the returned string, separated by spaces:

  ```
  util.format('%s:%s', 'foo', 'bar', 'baz');
  // Returns: 'foo:bar baz'
  ```

  If the first argument does not contain a valid format specifier, `util.format()` returns a string that is the concatenation of all arguments separated by spaces:

  ```
  util.format(1, 2, 3);
  // Returns: '1 2 3'
  ```

  If only one argument is passed to `util.format()`, it is returned as it is without any formatting:

  ```
  util.format('%% %s');
  // Returns: '%% %s'
  ```

  `util.format()` is a synchronous method that is intended as a debugging tool. Some input values can have a significant performance overhead that can block the event loop. Use this function with care and never in a hot code path.

  @param format

  A `printf`-like format string.
* function [formatWithOptions](https://bun.com/reference/node/util/formatWithOptions)(

  inspectOptions: [InspectOptions](https://bun.com/reference/node/util/InspectOptions),

  format?: any,

  ...param: any[]

  ): string;

  This function is identical to format, except in that it takes an `inspectOptions` argument which specifies options that are passed along to inspect.

  ```
  util.formatWithOptions({ colors: true }, 'See object %O', { foo: 42 });
  // Returns 'See object { foo: 42 }', where `42` is colored as a number
  // when printed to a terminal.
  ```
* function [getCallSites](https://bun.com/reference/node/util/getCallSites)(

  frameCount?: number,

  options?: GetCallSitesOptions

  ): [CallSiteObject](https://bun.com/reference/node/util/CallSiteObject)[];

  Returns an array of call site objects containing the stack of the caller function.

  ```
  import { getCallSites } from 'node:util';

  function exampleFunction() {
    const callSites = getCallSites();

    console.log('Call Sites:');
    callSites.forEach((callSite, index) => {
      console.log(`CallSite ${index + 1}:`);
      console.log(`Function Name: ${callSite.functionName}`);
      console.log(`Script Name: ${callSite.scriptName}`);
      console.log(`Line Number: ${callSite.lineNumber}`);
      console.log(`Column Number: ${callSite.column}`);
    });
    // CallSite 1:
    // Function Name: exampleFunction
    // Script Name: /home/example.js
    // Line Number: 5
    // Column Number: 26

    // CallSite 2:
    // Function Name: anotherFunction
    // Script Name: /home/example.js
    // Line Number: 22
    // Column Number: 3

    // ...
  }

  // A function to simulate another stack layer
  function anotherFunction() {
    exampleFunction();
  }

  anotherFunction();
  ```

  It is possible to reconstruct the original locations by setting the option `sourceMap` to `true`. If the source map is not available, the original location will be the same as the current location. When the `--enable-source-maps` flag is enabled, for example when using `--experimental-transform-types`, `sourceMap` will be true by default.

  ```
  import { getCallSites } from 'node:util';

  interface Foo {
    foo: string;
  }

  const callSites = getCallSites({ sourceMap: true });

  // With sourceMap:
  // Function Name: ''
  // Script Name: example.js
  // Line Number: 7
  // Column Number: 26

  // Without sourceMap:
  // Function Name: ''
  // Script Name: example.js
  // Line Number: 2
  // Column Number: 26
  ```

  @param frameCount

  Number of frames to capture as call site objects. **Default:** `10`. Allowable range is between 1 and 200.

  @returns

  An array of call site objects

  function [getCallSites](https://bun.com/reference/node/util/getCallSites)(

  options: GetCallSitesOptions

  ): [CallSiteObject](https://bun.com/reference/node/util/CallSiteObject)[];

  Returns an array of call site objects containing the stack of the caller function.

  ```
  import { getCallSites } from 'node:util';

  function exampleFunction() {
    const callSites = getCallSites();

    console.log('Call Sites:');
    callSites.forEach((callSite, index) => {
      console.log(`CallSite ${index + 1}:`);
      console.log(`Function Name: ${callSite.functionName}`);
      console.log(`Script Name: ${callSite.scriptName}`);
      console.log(`Line Number: ${callSite.lineNumber}`);
      console.log(`Column Number: ${callSite.column}`);
    });
    // CallSite 1:
    // Function Name: exampleFunction
    // Script Name: /home/example.js
    // Line Number: 5
    // Column Number: 26

    // CallSite 2:
    // Function Name: anotherFunction
    // Script Name: /home/example.js
    // Line Number: 22
    // Column Number: 3

    // ...
  }

  // A function to simulate another stack layer
  function anotherFunction() {
    exampleFunction();
  }

  anotherFunction();
  ```

  It is possible to reconstruct the original locations by setting the option `sourceMap` to `true`. If the source map is not available, the original location will be the same as the current location. When the `--enable-source-maps` flag is enabled, for example when using `--experimental-transform-types`, `sourceMap` will be true by default.

  ```
  import { getCallSites } from 'node:util';

  interface Foo {
    foo: string;
  }

  const callSites = getCallSites({ sourceMap: true });

  // With sourceMap:
  // Function Name: ''
  // Script Name: example.js
  // Line Number: 7
  // Column Number: 26

  // Without sourceMap:
  // Function Name: ''
  // Script Name: example.js
  // Line Number: 2
  // Column Number: 26
  ```

  @returns

  An array of call site objects
* function [getSystemErrorMap](https://bun.com/reference/node/util/getSystemErrorMap)(): Map<number, [string, string]>;

  Returns a Map of all system error codes available from the Node.js API. The mapping between error codes and error names is platform-dependent. See `Common System Errors` for the names of common errors.

  ```
  fs.access('file/that/does/not/exist', (err) => {
    const errorMap = util.getSystemErrorMap();
    const name = errorMap.get(err.errno);
    console.error(name);  // ENOENT
  });
  ```
* function [getSystemErrorMessage](https://bun.com/reference/node/util/getSystemErrorMessage)(

  err: number

  ): string;

  Returns the string message for a numeric error code that comes from a Node.js API. The mapping between error codes and string messages is platform-dependent.

  ```
  fs.access('file/that/does/not/exist', (err) => {
    const message = util.getSystemErrorMessage(err.errno);
    console.error(message);  // no such file or directory
  });
  ```
* function [getSystemErrorName](https://bun.com/reference/node/util/getSystemErrorName)(

  err: number

  ): string;

  Returns the string name for a numeric error code that comes from a Node.js API. The mapping between error codes and error names is platform-dependent. See `Common System Errors` for the names of common errors.

  ```
  fs.access('file/that/does/not/exist', (err) => {
    const name = util.getSystemErrorName(err.errno);
    console.error(name);  // ENOENT
  });
  ```
* function [inherits](https://bun.com/reference/node/util/inherits)(

  constructor: unknown,

  superConstructor: unknown

  ): void;

  Usage of `util.inherits()` is discouraged. Please use the ES6 `class` and `extends` keywords to get language level inheritance support. Also note that the two styles are [semantically incompatible](https://github.com/nodejs/node/issues/4179).

  Inherit the prototype methods from one [constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) into another. The prototype of `constructor` will be set to a new object created from `superConstructor`.

  This mainly adds some input validation on top of `Object.setPrototypeOf(constructor.prototype, superConstructor.prototype)`. As an additional convenience, `superConstructor` will be accessible through the `constructor.super_` property.

  ```
  const util = require('node:util');
  const EventEmitter = require('node:events');

  function MyStream() {
    EventEmitter.call(this);
  }

  util.inherits(MyStream, EventEmitter);

  MyStream.prototype.write = function(data) {
    this.emit('data', data);
  };

  const stream = new MyStream();

  console.log(stream instanceof EventEmitter); // true
  console.log(MyStream.super_ === EventEmitter); // true

  stream.on('data', (data) => {
    console.log(`Received data: "${data}"`);
  });
  stream.write('It works!'); // Received data: "It works!"
  ```

  ES6 example using `class` and `extends`:

  ```
  import EventEmitter from 'node:events';

  class MyStream extends EventEmitter {
    write(data) {
      this.emit('data', data);
    }
  }

  const stream = new MyStream();

  stream.on('data', (data) => {
    console.log(`Received data: "${data}"`);
  });
  stream.write('With ES6');
  ```
* function [inspect](https://bun.com/reference/node/util/inspect)(

  object: any,

  showHidden?: boolean,

  depth?: null | number,

  color?: boolean

  ): string;

  The `util.inspect()` method returns a string representation of `object` that is intended for debugging. The output of `util.inspect` may change at any time and should not be depended upon programmatically. Additional `options` may be passed that alter the result. `util.inspect()` will use the constructor's name and/or `Symbol.toStringTag` property to make an identifiable tag for an inspected value.

  ```
  class Foo {
    get [Symbol.toStringTag]() {
      return 'bar';
    }
  }

  class Bar {}

  const baz = Object.create(null, { [Symbol.toStringTag]: { value: 'foo' } });

  util.inspect(new Foo()); // 'Foo [bar] {}'
  util.inspect(new Bar()); // 'Bar {}'
  util.inspect(baz);       // '[foo] {}'
  ```

  Circular references point to their anchor by using a reference index:

  ```
  import { inspect } from 'node:util';

  const obj = {};
  obj.a = [obj];
  obj.b = {};
  obj.b.inner = obj.b;
  obj.b.obj = obj;

  console.log(inspect(obj));
  // <ref *1> {
  //   a: [ [Circular *1] ],
  //   b: <ref *2> { inner: [Circular *2], obj: [Circular *1] }
  // }
  ```

  The following example inspects all properties of the `util` object:

  ```
  import util from 'node:util';

  console.log(util.inspect(util, { showHidden: true, depth: null }));
  ```

  The following example highlights the effect of the `compact` option:

  ```
  import { inspect } from 'node:util';

  const o = {
    a: [1, 2, [[
      'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit, sed do ' +
        'eiusmod \ntempor incididunt ut labore et dolore magna aliqua.',
      'test',
      'foo']], 4],
    b: new Map([['za', 1], ['zb', 'test']]),
  };
  console.log(inspect(o, { compact: true, depth: 5, breakLength: 80 }));

  // { a:
  //   [ 1,
  //     2,
  //     [ [ 'Lorem ipsum dolor sit amet,\nconsectetur [...]', // A long line
  //           'test',
  //           'foo' ] ],
  //     4 ],
  //   b: Map(2) { 'za' => 1, 'zb' => 'test' } }

  // Setting `compact` to false or an integer creates more reader friendly output.
  console.log(inspect(o, { compact: false, depth: 5, breakLength: 80 }));

  // {
  //   a: [
  //     1,
  //     2,
  //     [
  //       [
  //         'Lorem ipsum dolor sit amet,\n' +
  //           'consectetur adipiscing elit, sed do eiusmod \n' +
  //           'tempor incididunt ut labore et dolore magna aliqua.',
  //         'test',
  //         'foo'
  //       ]
  //     ],
  //     4
  //   ],
  //   b: Map(2) {
  //     'za' => 1,
  //     'zb' => 'test'
  //   }
  // }

  // Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
  // single line.
  ```

  The `showHidden` option allows `WeakMap` and `WeakSet` entries to be inspected. If there are more entries than `maxArrayLength`, there is no guarantee which entries are displayed. That means retrieving the same `WeakSet` entries twice may result in different output. Furthermore, entries with no remaining strong references may be garbage collected at any time.

  ```
  import { inspect } from 'node:util';

  const obj = { a: 1 };
  const obj2 = { b: 2 };
  const weakSet = new WeakSet([obj, obj2]);

  console.log(inspect(weakSet, { showHidden: true }));
  // WeakSet { { a: 1 }, { b: 2 } }
  ```

  The `sorted` option ensures that an object's property insertion order does not impact the result of `util.inspect()`.

  ```
  import { inspect } from 'node:util';
  import assert from 'node:assert';

  const o1 = {
    b: [2, 3, 1],
    a: '`a` comes before `b`',
    c: new Set([2, 3, 1]),
  };
  console.log(inspect(o1, { sorted: true }));
  // { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set(3) { 1, 2, 3 } }
  console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
  // { c: Set(3) { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

  const o2 = {
    c: new Set([2, 1, 3]),
    a: '`a` comes before `b`',
    b: [2, 3, 1],
  };
  assert.strict.equal(
    inspect(o1, { sorted: true }),
    inspect(o2, { sorted: true }),
  );
  ```

  The `numericSeparator` option adds an underscore every three digits to all numbers.

  ```
  import { inspect } from 'node:util';

  const thousand = 1000;
  const million = 1000000;
  const bigNumber = 123456789n;
  const bigDecimal = 1234.12345;

  console.log(inspect(thousand, { numericSeparator: true }));
  // 1_000
  console.log(inspect(million, { numericSeparator: true }));
  // 1_000_000
  console.log(inspect(bigNumber, { numericSeparator: true }));
  // 123_456_789n
  console.log(inspect(bigDecimal, { numericSeparator: true }));
  // 1_234.123_45
  ```

  `util.inspect()` is a synchronous method intended for debugging. Its maximum output length is approximately 128 MiB. Inputs that result in longer output will be truncated.

  @param object

  Any JavaScript primitive or `Object`.

  @returns

  The representation of `object`.

  function [inspect](https://bun.com/reference/node/util/inspect)(

  object: any,

  options?: [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

  ): string;

  The `util.inspect()` method returns a string representation of `object` that is intended for debugging. The output of `util.inspect` may change at any time and should not be depended upon programmatically. Additional `options` may be passed that alter the result. `util.inspect()` will use the constructor's name and/or `Symbol.toStringTag` property to make an identifiable tag for an inspected value.

  ```
  class Foo {
    get [Symbol.toStringTag]() {
      return 'bar';
    }
  }

  class Bar {}

  const baz = Object.create(null, { [Symbol.toStringTag]: { value: 'foo' } });

  util.inspect(new Foo()); // 'Foo [bar] {}'
  util.inspect(new Bar()); // 'Bar {}'
  util.inspect(baz);       // '[foo] {}'
  ```

  Circular references point to their anchor by using a reference index:

  ```
  import { inspect } from 'node:util';

  const obj = {};
  obj.a = [obj];
  obj.b = {};
  obj.b.inner = obj.b;
  obj.b.obj = obj;

  console.log(inspect(obj));
  // <ref *1> {
  //   a: [ [Circular *1] ],
  //   b: <ref *2> { inner: [Circular *2], obj: [Circular *1] }
  // }
  ```

  The following example inspects all properties of the `util` object:

  ```
  import util from 'node:util';

  console.log(util.inspect(util, { showHidden: true, depth: null }));
  ```

  The following example highlights the effect of the `compact` option:

  ```
  import { inspect } from 'node:util';

  const o = {
    a: [1, 2, [[
      'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit, sed do ' +
        'eiusmod \ntempor incididunt ut labore et dolore magna aliqua.',
      'test',
      'foo']], 4],
    b: new Map([['za', 1], ['zb', 'test']]),
  };
  console.log(inspect(o, { compact: true, depth: 5, breakLength: 80 }));

  // { a:
  //   [ 1,
  //     2,
  //     [ [ 'Lorem ipsum dolor sit amet,\nconsectetur [...]', // A long line
  //           'test',
  //           'foo' ] ],
  //     4 ],
  //   b: Map(2) { 'za' => 1, 'zb' => 'test' } }

  // Setting `compact` to false or an integer creates more reader friendly output.
  console.log(inspect(o, { compact: false, depth: 5, breakLength: 80 }));

  // {
  //   a: [
  //     1,
  //     2,
  //     [
  //       [
  //         'Lorem ipsum dolor sit amet,\n' +
  //           'consectetur adipiscing elit, sed do eiusmod \n' +
  //           'tempor incididunt ut labore et dolore magna aliqua.',
  //         'test',
  //         'foo'
  //       ]
  //     ],
  //     4
  //   ],
  //   b: Map(2) {
  //     'za' => 1,
  //     'zb' => 'test'
  //   }
  // }

  // Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
  // single line.
  ```

  The `showHidden` option allows `WeakMap` and `WeakSet` entries to be inspected. If there are more entries than `maxArrayLength`, there is no guarantee which entries are displayed. That means retrieving the same `WeakSet` entries twice may result in different output. Furthermore, entries with no remaining strong references may be garbage collected at any time.

  ```
  import { inspect } from 'node:util';

  const obj = { a: 1 };
  const obj2 = { b: 2 };
  const weakSet = new WeakSet([obj, obj2]);

  console.log(inspect(weakSet, { showHidden: true }));
  // WeakSet { { a: 1 }, { b: 2 } }
  ```

  The `sorted` option ensures that an object's property insertion order does not impact the result of `util.inspect()`.

  ```
  import { inspect } from 'node:util';
  import assert from 'node:assert';

  const o1 = {
    b: [2, 3, 1],
    a: '`a` comes before `b`',
    c: new Set([2, 3, 1]),
  };
  console.log(inspect(o1, { sorted: true }));
  // { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set(3) { 1, 2, 3 } }
  console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
  // { c: Set(3) { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

  const o2 = {
    c: new Set([2, 1, 3]),
    a: '`a` comes before `b`',
    b: [2, 3, 1],
  };
  assert.strict.equal(
    inspect(o1, { sorted: true }),
    inspect(o2, { sorted: true }),
  );
  ```

  The `numericSeparator` option adds an underscore every three digits to all numbers.

  ```
  import { inspect } from 'node:util';

  const thousand = 1000;
  const million = 1000000;
  const bigNumber = 123456789n;
  const bigDecimal = 1234.12345;

  console.log(inspect(thousand, { numericSeparator: true }));
  // 1_000
  console.log(inspect(million, { numericSeparator: true }));
  // 1_000_000
  console.log(inspect(bigNumber, { numericSeparator: true }));
  // 123_456_789n
  console.log(inspect(bigDecimal, { numericSeparator: true }));
  // 1_234.123_45
  ```

  `util.inspect()` is a synchronous method intended for debugging. Its maximum output length is approximately 128 MiB. Inputs that result in longer output will be truncated.

  @param object

  Any JavaScript primitive or `Object`.

  @returns

  The representation of `object`.

  const [colors](https://bun.com/reference/node/util/inspect/colors): NodeJS.Dict<[number, number]>

  const [custom](https://bun.com/reference/node/util/inspect/custom): unique symbol

  That can be used to declare custom inspect functions.

  const [defaultOptions](https://bun.com/reference/node/util/inspect/defaultOptions): [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

  const [replDefaults](https://bun.com/reference/node/util/inspect/replDefaults): [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

  Allows changing inspect settings from the repl.

  const [styles](https://bun.com/reference/node/util/inspect/styles): { [K in [Style](https://bun.com/reference/node/util/Style)]: string }
* function [isDeepStrictEqual](https://bun.com/reference/node/util/isDeepStrictEqual)(

  val1: unknown,

  val2: unknown,

  options?: [IsDeepStrictEqualOptions](https://bun.com/reference/node/util/IsDeepStrictEqualOptions)

  ): boolean;

  Returns `true` if there is deep strict equality between `val1` and `val2`. Otherwise, returns `false`.

  See `assert.deepStrictEqual()` for more information about deep strict equality.
* function [parseArgs](https://bun.com/reference/node/util/parseArgs)<T extends [ParseArgsConfig](https://bun.com/reference/node/util/ParseArgsConfig)>(

  config?: T

  ): ParsedResults<T>;

  Provides a higher level API for command-line argument parsing than interacting with `process.argv` directly. Takes a specification for the expected arguments and returns a structured object with the parsed options and positionals.

  ```
  import { parseArgs } from 'node:util';
  const args = ['-f', '--bar', 'b'];
  const options = {
    foo: {
      type: 'boolean',
      short: 'f',
    },
    bar: {
      type: 'string',
    },
  };
  const {
    values,
    positionals,
  } = parseArgs({ args, options });
  console.log(values, positionals);
  // Prints: [Object: null prototype] { foo: true, bar: 'b' } []
  ```

  @param config

  Used to provide arguments for parsing and to configure the parser. `config` supports the following properties:

  @returns

  The parsed command line arguments:
* function [parseEnv](https://bun.com/reference/node/util/parseEnv)(

  content: string

  ): Dict<string>;

  Stability: 1.1 - Active development Given an example `.env` file:

  ```
  import { parseEnv } from 'node:util';

  parseEnv('HELLO=world\nHELLO=oh my\n');
  // Returns: { HELLO: 'oh my' }
  ```

  @param content

  The raw contents of a `.env` file.
* function [promisify](https://bun.com/reference/node/util/promisify)<TCustom extends Function>(

  fn: [CustomPromisify](https://bun.com/reference/node/util/CustomPromisify)<TCustom>

  ): TCustom;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<TResult>(

  fn: (callback: (err: any, result: TResult) => void) => void

  ): () => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)(

  fn: (callback: (err?: any) => void) => void

  ): () => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, TResult>(

  fn: (arg1: T1, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1>(

  fn: (arg1: T1, callback: (err?: any) => void) => void

  ): (arg1: T1) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, TResult>(

  fn: (arg1: T1, arg2: T2, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2>(

  fn: (arg1: T1, arg2: T2, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3>(

  fn: (arg1: T1, arg2: T2, arg3: T3, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, T5, TResult>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err: any, result: TResult) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<TResult>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)<T1, T2, T3, T4, T5>(

  fn: (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5, callback: (err?: any) => void) => void

  ): (arg1: T1, arg2: T2, arg3: T3, arg4: T4, arg5: T5) => Promise<void>;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  function [promisify](https://bun.com/reference/node/util/promisify)(

  fn: Function

  ): Function;

  Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the last argument, and returns a version that returns promises.

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);
  promisifiedStat('.').then((stats) => {
    // Do something with `stats`
  }).catch((error) => {
    // Handle the error.
  });
  ```

  Or, equivalently using `async function`s:

  ```
  import { promisify } from 'node:util';
  import { stat } from 'node:fs';

  const promisifiedStat = promisify(stat);

  async function callStat() {
    const stats = await promisifiedStat('.');
    console.log(`This directory is owned by ${stats.uid}`);
  }

  callStat();
  ```

  If there is an `original[util.promisify.custom]` property present, `promisify` will return its value, see [Custom promisified functions](https://nodejs.org/docs/latest-v24.x/api/util.html#custom-promisified-functions).

  `promisify()` assumes that `original` is a function taking a callback as its final argument in all cases. If `original` is not a function, `promisify()` will throw an error. If `original` is a function but its last argument is not an error-first callback, it will still be passed an error-first callback as its last argument.

  Using `promisify()` on class methods or other methods that use `this` may not work as expected unless handled specially:

  ```
  import { promisify } from 'node:util';

  class Foo {
    constructor() {
      this.a = 42;
    }

    bar(callback) {
      callback(null, this.a);
    }
  }

  const foo = new Foo();

  const naiveBar = promisify(foo.bar);
  // TypeError: Cannot read properties of undefined (reading 'a')
  // naiveBar().then(a => console.log(a));

  naiveBar.call(foo).then((a) => console.log(a)); // '42'

  const bindBar = naiveBar.bind(foo);
  bindBar().then((a) => console.log(a)); // '42'
  ```

  const [custom](https://bun.com/reference/node/util/promisify/custom): unique symbol

  That can be used to declare custom promisified variants of functions.
* function [setTraceSigInt](https://bun.com/reference/node/util/setTraceSigInt)(

  enable: boolean

  ): void;

  Enable or disable printing a stack trace on `SIGINT`. The API is only available on the main thread.
* function [stripVTControlCharacters](https://bun.com/reference/node/util/stripVTControlCharacters)(

  str: string

  ): string;

  Returns `str` with any ANSI escape codes removed.

  ```
  console.log(util.stripVTControlCharacters('\u001B[4mvalue\u001B[0m'));
  // Prints "value"
  ```
* function [styleText](https://bun.com/reference/node/util/styleText)(

  format: ForegroundColors | BackgroundColors | Modifiers | unknown[],

  text: string,

  options?: [StyleTextOptions](https://bun.com/reference/node/util/StyleTextOptions)

  ): string;

  This function returns a formatted text considering the `format` passed for printing in a terminal. It is aware of the terminal's capabilities and acts according to the configuration set via `NO_COLOR`, `NODE_DISABLE_COLORS` and `FORCE_COLOR` environment variables.

  ```
  import { styleText } from 'node:util';
  import { stderr } from 'node:process';

  const successMessage = styleText('green', 'Success!');
  console.log(successMessage);

  const errorMessage = styleText(
    'red',
    'Error! Error!',
    // Validate if process.stderr has TTY
    { stream: stderr },
  );
  console.error(errorMessage);
  ```

  `util.inspect.colors` also provides text formats such as `italic`, and `underline` and you can combine both:

  ```
  console.log(
    util.styleText(['underline', 'italic'], 'My italic underlined message'),
  );
  ```

  When passing an array of formats, the order of the format applied is left to right so the following style might overwrite the previous one.

  ```
  console.log(
    util.styleText(['red', 'green'], 'text'), // green
  );
  ```

  The special format value `none` applies no additional styling to the text.

  The full list of formats can be found in [modifiers](https://nodejs.org/docs/latest-v24.x/api/util.html#modifiers).

  @param format

  A text format or an Array of text formats defined in `util.inspect.colors`.

  @param text

  The text to to be formatted.
* function [toUSVString](https://bun.com/reference/node/util/toUSVString)(

  string: string

  ): string;

  Returns the `string` after replacing any surrogate code points (or equivalently, any unpaired surrogate code units) with the Unicode "replacement character" U+FFFD.
* function [transferableAbortController](https://bun.com/reference/node/util/transferableAbortController)(): [AbortController](https://bun.com/reference/globals/AbortController);

  Creates and returns an `AbortController` instance whose `AbortSignal` is marked as transferable and can be used with `structuredClone()` or `postMessage()`.

  @returns

  A transferable AbortController
* function [transferableAbortSignal](https://bun.com/reference/node/util/transferableAbortSignal)(

  signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

  ): [AbortSignal](https://bun.com/reference/globals/AbortSignal);

  Marks the given `AbortSignal` as transferable so that it can be used with`structuredClone()` and `postMessage()`.

  ```
  const signal = transferableAbortSignal(AbortSignal.timeout(100));
  const channel = new MessageChannel();
  channel.port2.postMessage(signal, [signal]);
  ```

  @param signal

  The AbortSignal

  @returns

  The same AbortSignal

## Type definitions

* ### interface [CallSiteObject](https://bun.com/reference/node/util/CallSiteObject)

  + [columnNumber](https://bun.com/reference/node/util/CallSiteObject/columnNumber): number

    Returns the 1-based column offset on the line for the associated function call.
  + [functionName](https://bun.com/reference/node/util/CallSiteObject/functionName): string

    Returns the name of the function associated with this call site.
  + [lineNumber](https://bun.com/reference/node/util/CallSiteObject/lineNumber): number

    Returns the number, 1-based, of the line for the associate function call.
  + [scriptId](https://bun.com/reference/node/util/CallSiteObject/scriptId): string

    Returns the unique id of the script, as in Chrome DevTools protocol [`Runtime.ScriptId`](https://chromedevtools.github.io/devtools-protocol/1-3/Runtime/#type-ScriptId).
  + [scriptName](https://bun.com/reference/node/util/CallSiteObject/scriptName): string

    Returns the name of the resource that contains the script for the function for this call site.
* ### interface [CustomPromisifyLegacy](https://bun.com/reference/node/util/CustomPromisifyLegacy)<TCustom extends Function>

  + [[metadata]](https://bun.com/reference/node/util/CustomPromisifyLegacy/[metadata]): null | DecoratorMetadataObject
  + [arguments](https://bun.com/reference/node/util/CustomPromisifyLegacy/arguments): any
  + [caller](https://bun.com/reference/node/util/CustomPromisifyLegacy/caller): Function
  + readonly [length](https://bun.com/reference/node/util/CustomPromisifyLegacy/length): number
  + readonly [name](https://bun.com/reference/node/util/CustomPromisifyLegacy/name): string

    Returns the name of the function. Function names are read-only and can not be changed.
  + [prototype](https://bun.com/reference/node/util/CustomPromisifyLegacy/prototype): any
  + [[Symbol.hasInstance]](https://bun.com/reference/node/util/CustomPromisifyLegacy/[hasInstance])(

    value: any

    ): boolean;

    Determines whether the given value inherits from this function if this function was used as a constructor function.

    A constructor function can control which objects are recognized as its instances by 'instanceof' by overriding this method.
  + [apply](https://bun.com/reference/node/util/CustomPromisifyLegacy/apply)(

    this: Function,

    thisArg: any,

    argArray?: any

    ): any;

    Calls the function, substituting the specified object for the this value of the function, and the specified array for the arguments of the function.

    @param thisArg

    The object to be used as the this object.

    @param argArray

    A set of arguments to be passed to the function.
  + [bind](https://bun.com/reference/node/util/CustomPromisifyLegacy/bind)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    For a given function, creates a bound function that has the same body as the original function. The this object of the bound function is associated with the specified object, and has the specified initial parameters.

    @param thisArg

    An object to which the this keyword can refer inside the new function.

    @param argArray

    A list of arguments to be passed to the new function.
  + [call](https://bun.com/reference/node/util/CustomPromisifyLegacy/call)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    Calls a method of an object, substituting another object for the current object.

    @param thisArg

    The object to be used as the current object.

    @param argArray

    A list of arguments to be passed to the method.
  + [toString](https://bun.com/reference/node/util/CustomPromisifyLegacy/toString)(): string;

    Returns a string representation of a function.
* ### interface [CustomPromisifySymbol](https://bun.com/reference/node/util/CustomPromisifySymbol)<TCustom extends Function>

  + [[custom]](https://bun.com/reference/node/util/CustomPromisifySymbol/[custom]): TCustom
  + [[metadata]](https://bun.com/reference/node/util/CustomPromisifySymbol/[metadata]): null | DecoratorMetadataObject
  + [arguments](https://bun.com/reference/node/util/CustomPromisifySymbol/arguments): any
  + [caller](https://bun.com/reference/node/util/CustomPromisifySymbol/caller): Function
  + readonly [length](https://bun.com/reference/node/util/CustomPromisifySymbol/length): number
  + readonly [name](https://bun.com/reference/node/util/CustomPromisifySymbol/name): string

    Returns the name of the function. Function names are read-only and can not be changed.
  + [prototype](https://bun.com/reference/node/util/CustomPromisifySymbol/prototype): any
  + [[Symbol.hasInstance]](https://bun.com/reference/node/util/CustomPromisifySymbol/[hasInstance])(

    value: any

    ): boolean;

    Determines whether the given value inherits from this function if this function was used as a constructor function.

    A constructor function can control which objects are recognized as its instances by 'instanceof' by overriding this method.
  + [apply](https://bun.com/reference/node/util/CustomPromisifySymbol/apply)(

    this: Function,

    thisArg: any,

    argArray?: any

    ): any;

    Calls the function, substituting the specified object for the this value of the function, and the specified array for the arguments of the function.

    @param thisArg

    The object to be used as the this object.

    @param argArray

    A set of arguments to be passed to the function.
  + [bind](https://bun.com/reference/node/util/CustomPromisifySymbol/bind)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    For a given function, creates a bound function that has the same body as the original function. The this object of the bound function is associated with the specified object, and has the specified initial parameters.

    @param thisArg

    An object to which the this keyword can refer inside the new function.

    @param argArray

    A list of arguments to be passed to the new function.
  + [call](https://bun.com/reference/node/util/CustomPromisifySymbol/call)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    Calls a method of an object, substituting another object for the current object.

    @param thisArg

    The object to be used as the current object.

    @param argArray

    A list of arguments to be passed to the method.
  + [toString](https://bun.com/reference/node/util/CustomPromisifySymbol/toString)(): string;

    Returns a string representation of a function.
* ### interface [DebugLogger](https://bun.com/reference/node/util/DebugLogger)

  + [enabled](https://bun.com/reference/node/util/DebugLogger/enabled): boolean

    The `util.debuglog().enabled` getter is used to create a test that can be used in conditionals based on the existence of the `NODE_DEBUG` environment variable. If the `section` name appears within the value of that environment variable, then the returned value will be `true`. If not, then the returned value will be `false`.

    ```
    import { debuglog } from 'node:util';
    const enabled = debuglog('foo').enabled;
    if (enabled) {
      console.log('hello from foo [%d]', 123);
    }
    ```

    If this program is run with `NODE_DEBUG=foo` in the environment, then it will output something like:

    ```
    hello from foo [123]
    ```
* ### interface [EncodeIntoResult](https://bun.com/reference/node/util/EncodeIntoResult)

  + [read](https://bun.com/reference/node/util/EncodeIntoResult/read): number

    The read Unicode code units of input.
  + [written](https://bun.com/reference/node/util/EncodeIntoResult/written): number

    The written UTF-8 bytes of output.
* ### interface [InspectOptions](https://bun.com/reference/node/util/InspectOptions)

  + [breakLength](https://bun.com/reference/node/util/InspectOptions/breakLength)?: number

    The length at which input values are split across multiple lines. Set to `Infinity` to format the input as a single line (in combination with `compact` set to `true` or any number >= `1`).
  + [colors](https://bun.com/reference/node/util/InspectOptions/colors)?: boolean

    If `true`, the output is styled with ANSI color codes. Colors are customizable.
  + [compact](https://bun.com/reference/node/util/InspectOptions/compact)?: number | boolean

    Setting this to `false` causes each object key to be displayed on a new line. It will also add new lines to text that is longer than `breakLength`. If set to a number, the most `n` inner elements are united on a single line as long as all properties fit into `breakLength`. Short array elements are also grouped together. Note that no text will be reduced below 16 characters, no matter the `breakLength` size. For more information, see the example below.
  + [customInspect](https://bun.com/reference/node/util/InspectOptions/customInspect)?: boolean

    If `false`, `[util.inspect.custom](depth, opts, inspect)` functions are not invoked.
  + [depth](https://bun.com/reference/node/util/InspectOptions/depth)?: null | number

    Specifies the number of times to recurse while formatting object. This is useful for inspecting large objects. To recurse up to the maximum call stack size pass `Infinity` or `null`.
  + [getters](https://bun.com/reference/node/util/InspectOptions/getters)?: boolean | 'get' | 'set'

    If set to `true`, getters are going to be inspected as well. If set to `'get'` only getters without setter are going to be inspected. If set to `'set'` only getters having a corresponding setter are going to be inspected. This might cause side effects depending on the getter function.
  + [maxArrayLength](https://bun.com/reference/node/util/InspectOptions/maxArrayLength)?: null | number

    Specifies the maximum number of `Array`, `TypedArray`, `WeakMap`, and `WeakSet` elements to include when formatting. Set to `null` or `Infinity` to show all elements. Set to `0` or negative to show no elements.
  + [maxStringLength](https://bun.com/reference/node/util/InspectOptions/maxStringLength)?: null | number

    Specifies the maximum number of characters to include when formatting. Set to `null` or `Infinity` to show all elements. Set to `0` or negative to show no characters.
  + [numericSeparator](https://bun.com/reference/node/util/InspectOptions/numericSeparator)?: boolean

    If set to `true`, an underscore is used to separate every three digits in all bigints and numbers.
  + [showHidden](https://bun.com/reference/node/util/InspectOptions/showHidden)?: boolean

    If `true`, object's non-enumerable symbols and properties are included in the formatted result. `WeakMap` and `WeakSet` entries are also included as well as user defined prototype properties (excluding method properties).
  + [showProxy](https://bun.com/reference/node/util/InspectOptions/showProxy)?: boolean

    If `true`, `Proxy` inspection includes the target and handler objects.
  + [sorted](https://bun.com/reference/node/util/InspectOptions/sorted)?: boolean | (a: string, b: string) => number

    If set to `true` or a function, all properties of an object, and `Set` and `Map` entries are sorted in the resulting string. If set to `true` the default sort is used. If set to a function, it is used as a compare function.
* ### interface [InspectOptionsStylized](https://bun.com/reference/node/util/InspectOptionsStylized)

  + [breakLength](https://bun.com/reference/node/util/InspectOptionsStylized/breakLength)?: number

    The length at which input values are split across multiple lines. Set to `Infinity` to format the input as a single line (in combination with `compact` set to `true` or any number >= `1`).
  + [colors](https://bun.com/reference/node/util/InspectOptionsStylized/colors)?: boolean

    If `true`, the output is styled with ANSI color codes. Colors are customizable.
  + [compact](https://bun.com/reference/node/util/InspectOptionsStylized/compact)?: number | boolean

    Setting this to `false` causes each object key to be displayed on a new line. It will also add new lines to text that is longer than `breakLength`. If set to a number, the most `n` inner elements are united on a single line as long as all properties fit into `breakLength`. Short array elements are also grouped together. Note that no text will be reduced below 16 characters, no matter the `breakLength` size. For more information, see the example below.
  + [customInspect](https://bun.com/reference/node/util/InspectOptionsStylized/customInspect)?: boolean

    If `false`, `[util.inspect.custom](depth, opts, inspect)` functions are not invoked.
  + [depth](https://bun.com/reference/node/util/InspectOptionsStylized/depth)?: null | number

    Specifies the number of times to recurse while formatting object. This is useful for inspecting large objects. To recurse up to the maximum call stack size pass `Infinity` or `null`.
  + [getters](https://bun.com/reference/node/util/InspectOptionsStylized/getters)?: boolean | 'get' | 'set'

    If set to `true`, getters are going to be inspected as well. If set to `'get'` only getters without setter are going to be inspected. If set to `'set'` only getters having a corresponding setter are going to be inspected. This might cause side effects depending on the getter function.
  + [maxArrayLength](https://bun.com/reference/node/util/InspectOptionsStylized/maxArrayLength)?: null | number

    Specifies the maximum number of `Array`, `TypedArray`, `WeakMap`, and `WeakSet` elements to include when formatting. Set to `null` or `Infinity` to show all elements. Set to `0` or negative to show no elements.
  + [maxStringLength](https://bun.com/reference/node/util/InspectOptionsStylized/maxStringLength)?: null | number

    Specifies the maximum number of characters to include when formatting. Set to `null` or `Infinity` to show all elements. Set to `0` or negative to show no characters.
  + [numericSeparator](https://bun.com/reference/node/util/InspectOptionsStylized/numericSeparator)?: boolean

    If set to `true`, an underscore is used to separate every three digits in all bigints and numbers.
  + [showHidden](https://bun.com/reference/node/util/InspectOptionsStylized/showHidden)?: boolean

    If `true`, object's non-enumerable symbols and properties are included in the formatted result. `WeakMap` and `WeakSet` entries are also included as well as user defined prototype properties (excluding method properties).
  + [showProxy](https://bun.com/reference/node/util/InspectOptionsStylized/showProxy)?: boolean

    If `true`, `Proxy` inspection includes the target and handler objects.
  + [sorted](https://bun.com/reference/node/util/InspectOptionsStylized/sorted)?: boolean | (a: string, b: string) => number

    If set to `true` or a function, all properties of an object, and `Set` and `Map` entries are sorted in the resulting string. If set to `true` the default sort is used. If set to a function, it is used as a compare function.
  + [stylize](https://bun.com/reference/node/util/InspectOptionsStylized/stylize)(

    text: string,

    styleType: [Style](https://bun.com/reference/node/util/Style)

    ): string;
* ### interface [IsDeepStrictEqualOptions](https://bun.com/reference/node/util/IsDeepStrictEqualOptions)

  + [skipPrototype](https://bun.com/reference/node/util/IsDeepStrictEqualOptions/skipPrototype)?: boolean

    If `true`, prototype and constructor comparison is skipped during deep strict equality check.
* ### interface [ParseArgsConfig](https://bun.com/reference/node/util/ParseArgsConfig)

  + [allowNegative](https://bun.com/reference/node/util/ParseArgsConfig/allowNegative)?: boolean

    If `true`, allows explicitly setting boolean options to `false` by prefixing the option name with `--no-`.
  + [allowPositionals](https://bun.com/reference/node/util/ParseArgsConfig/allowPositionals)?: boolean

    Whether this command accepts positional arguments.
  + [args](https://bun.com/reference/node/util/ParseArgsConfig/args)?: readonly string[]

    Array of argument strings.
  + [options](https://bun.com/reference/node/util/ParseArgsConfig/options)?: [ParseArgsOptionsConfig](https://bun.com/reference/node/util/ParseArgsOptionsConfig)

    Used to describe arguments known to the parser.
  + [strict](https://bun.com/reference/node/util/ParseArgsConfig/strict)?: boolean

    Should an error be thrown when unknown arguments are encountered, or when arguments are passed that do not match the `type` configured in `options`.
  + [tokens](https://bun.com/reference/node/util/ParseArgsConfig/tokens)?: boolean

    Return the parsed tokens. This is useful for extending the built-in behavior, from adding additional checks through to reprocessing the tokens in different ways.
* ### interface [ParseArgsOptionDescriptor](https://bun.com/reference/node/util/ParseArgsOptionDescriptor)

  + [default](https://bun.com/reference/node/util/ParseArgsOptionDescriptor/default)?: string | boolean | string[] | boolean[]

    The value to assign to the option if it does not appear in the arguments to be parsed. The value must match the type specified by the `type` property. If `multiple` is `true`, it must be an array. No default value is applied when the option does appear in the arguments to be parsed, even if the provided value is falsy.
  + [multiple](https://bun.com/reference/node/util/ParseArgsOptionDescriptor/multiple)?: boolean

    Whether this option can be provided multiple times. If `true`, all values will be collected in an array. If `false`, values for the option are last-wins.
  + [short](https://bun.com/reference/node/util/ParseArgsOptionDescriptor/short)?: string

    A single character alias for the option.
  + [type](https://bun.com/reference/node/util/ParseArgsOptionDescriptor/type): [ParseArgsOptionsType](https://bun.com/reference/node/util/ParseArgsOptionsType)

    Type of argument.
* ### interface [ParseArgsOptionsConfig](https://bun.com/reference/node/util/ParseArgsOptionsConfig)
* ### interface [StyleTextOptions](https://bun.com/reference/node/util/StyleTextOptions)

  + [stream](https://bun.com/reference/node/util/StyleTextOptions/stream)?: WritableStream

    A stream that will be validated if it can be colored.
  + [validateStream](https://bun.com/reference/node/util/StyleTextOptions/validateStream)?: boolean

    When true, `stream` is checked to see if it can handle colors.
* type [CustomInspectFunction](https://bun.com/reference/node/util/CustomInspectFunction) = (depth: number, options: [InspectOptionsStylized](https://bun.com/reference/node/util/InspectOptionsStylized)) => any
* type [CustomPromisify](https://bun.com/reference/node/util/CustomPromisify)<TCustom extends Function> = [CustomPromisifySymbol](https://bun.com/reference/node/util/CustomPromisifySymbol)<TCustom> | [CustomPromisifyLegacy](https://bun.com/reference/node/util/CustomPromisifyLegacy)<TCustom>
* type [DebugLoggerFunction](https://bun.com/reference/node/util/DebugLoggerFunction) = (msg: string, ...param: unknown[]) => void
* type [DiffEntry](https://bun.com/reference/node/util/DiffEntry) = [operation: -1 | 0 | 1, value: string]
* type [ParseArgsOptionsType](https://bun.com/reference/node/util/ParseArgsOptionsType) = 'boolean' | 'string'

  Type of argument used in parseArgs.
* type [Style](https://bun.com/reference/node/util/Style) = 'special' | 'number' | 'bigint' | 'boolean' | 'undefined' | 'null' | 'string' | 'symbol' | 'date' | 'regexp' | 'module'