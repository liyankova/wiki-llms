---
url: https://bun.com/docs/bundler/minifier
title: Minifier - Bun
source_domain: bun.com
---

# Minifier - Bun

Bun includes a fast JavaScript and TypeScript minifier that can reduce bundle sizes by 80% or more (depending on the codebase) and make output code run faster. The minifier performs dozens of optimizations including constant folding, dead code elimination, and syntax transformations. Unlike other minifiers, Bun’s minifier makes `bun build` run faster since there’s less code to print.

## [​](https://bun.com/docs/bundler/minifier#cli-usage) CLI Usage

### [​](https://bun.com/docs/bundler/minifier#enable-all-minification) Enable all minification

Use the `--minify` flag to enable all minification modes:

Copy

```
bun build ./index.ts --minify --outfile=out.js
```

The `--minify` flag automatically enables:

* Whitespace minification
* Syntax minification
* Identifier minification

### [​](https://bun.com/docs/bundler/minifier#production-mode) Production mode

The `--production` flag automatically enables minification:

Copy

```
bun build ./index.ts --production --outfile=out.js
```

The `--production` flag also:

* Sets `process.env.NODE_ENV` to `production`
* Enables the production-mode JSX import & transform

### [​](https://bun.com/docs/bundler/minifier#granular-control) Granular control

You can enable specific minification modes individually:

Copy

```
# Only remove whitespace
bun build ./index.ts --minify-whitespace --outfile=out.js

# Only minify syntax
bun build ./index.ts --minify-syntax --outfile=out.js

# Only minify identifiers
bun build ./index.ts --minify-identifiers --outfile=out.js

# Combine specific modes
bun build ./index.ts --minify-whitespace --minify-syntax --outfile=out.js
```

## [​](https://bun.com/docs/bundler/minifier#javascript-api) JavaScript API

When using Bun’s bundler programmatically, configure minification through the `minify` option:

Copy

```
await Bun.build({
  entrypoints: ["./index.ts"],
  outdir: "./out",
  minify: true, // Enable all minification modes
});
```

For granular control, pass an object:

Copy

```
await Bun.build({
  entrypoints: ["./index.ts"],
  outdir: "./out",
  minify: {
    whitespace: true,
    syntax: true,
    identifiers: true,
  },
});
```

## [​](https://bun.com/docs/bundler/minifier#minification-modes) Minification Modes

Bun’s minifier has three independent modes that can be enabled separately or combined.

### [​](https://bun.com/docs/bundler/minifier#whitespace-minification-minify-whitespace) Whitespace minification (`--minify-whitespace`)

Removes all unnecessary whitespace, newlines, and formatting from the output.

### [​](https://bun.com/docs/bundler/minifier#syntax-minification-minify-syntax) Syntax minification (`--minify-syntax`)

Rewrites JavaScript syntax to shorter equivalent forms and performs constant folding, dead code elimination, and other optimizations.

### [​](https://bun.com/docs/bundler/minifier#identifier-minification-minify-identifiers) Identifier minification (`--minify-identifiers`)

Renames local variables and function names to shorter identifiers using frequency-based optimization.

## [​](https://bun.com/docs/bundler/minifier#all-transformations) All Transformations

### [​](https://bun.com/docs/bundler/minifier#boolean-literal-shortening) Boolean literal shortening

**Mode:** `--minify-syntax`
Converts boolean literals to shorter expressions.

Input

Copy

```
true
false
```

Output

Copy

```
!0
!1
```

### [​](https://bun.com/docs/bundler/minifier#boolean-algebra-optimizations) Boolean algebra optimizations

**Mode:** `--minify-syntax`
Simplifies boolean expressions using logical rules.

Input

Copy

```
!!x
x === true
x && true
x || false
!true
!false
```

Output

Copy

```
x
x
x
x
!1
!0
```

### [​](https://bun.com/docs/bundler/minifier#undefined-shortening) Undefined shortening

**Mode:** `--minify-syntax`
Replaces `undefined` with shorter equivalent.

Input

Copy

```
undefined
let x = undefined;
```

Output

Copy

```
void 0
let x=void 0;
```

### [​](https://bun.com/docs/bundler/minifier#undefined-equality-optimization) Undefined equality optimization

**Mode:** `--minify-syntax`
Optimizes loose equality checks with undefined.

Input

Copy

```
x == undefined
x != undefined
```

Output

Copy

```
x == null
x != null
```

### [​](https://bun.com/docs/bundler/minifier#infinity-shortening) Infinity shortening

**Mode:** `--minify-syntax`
Converts Infinity to mathematical expressions.

Input

Copy

```
Infinity
-Infinity
```

Output

Copy

```
1/0
-1/0
```

### [​](https://bun.com/docs/bundler/minifier#typeof-optimizations) Typeof optimizations

**Mode:** `--minify-syntax`
Optimizes typeof comparisons and evaluates constant typeof expressions.

Input

Copy

```
typeof x === 'undefined'
typeof x !== 'undefined'
typeof require
typeof null
typeof true
typeof 123
typeof "str"
typeof 123n
```

Output

Copy

```
typeof x>'u'
typeof x<'u'
"function"
"object"
"boolean"
"number"
"string"
"bigint"
```

### [​](https://bun.com/docs/bundler/minifier#number-formatting) Number formatting

**Mode:** `--minify-syntax`
Formats numbers in the most compact representation.

Input

Copy

```
10000
100000
1000000
1.0
-42.0
```

Output

Copy

```
1e4
1e5
1e6
1
-42
```

### [​](https://bun.com/docs/bundler/minifier#arithmetic-constant-folding) Arithmetic constant folding

**Mode:** `--minify-syntax`
Evaluates arithmetic operations at compile time.

Input

Copy

```
1 + 2
10 - 5
3 * 4
10 / 2
10 % 3
2 ** 3
```

Output

Copy

```
3
5
12
5
1
8
```

### [​](https://bun.com/docs/bundler/minifier#bitwise-constant-folding) Bitwise constant folding

**Mode:** `--minify-syntax`
Evaluates bitwise operations at compile time.

Input

Copy

```
5 & 3
5 | 3
5 ^ 3
8 << 2
32 >> 2
~5
```

Output

Copy

```
1
7
6
32
8
-6
```

### [​](https://bun.com/docs/bundler/minifier#string-concatenation) String concatenation

**Mode:** `--minify-syntax`
Combines string literals at compile time.

Input

Copy

```
"a" + "b"
"x" + 123
"foo" + "bar" + "baz"
```

Output

Copy

```
"ab"
"x123"
"foobarbaz"
```

### [​](https://bun.com/docs/bundler/minifier#string-indexing) String indexing

**Mode:** `--minify-syntax`
Evaluates string character access at compile time.

Input

Copy

```
"foo"[2]
"hello"[0]
```

Output

Copy

```
"o"
"h"
```

### [​](https://bun.com/docs/bundler/minifier#template-literal-folding) Template literal folding

**Mode:** `--minify-syntax`
Evaluates template literals with constant expressions.

Input

Copy

```
`a${123}b`
`result: ${5 + 10}`
```

Output

Copy

```
"a123b"
"result: 15"
```

### [​](https://bun.com/docs/bundler/minifier#template-literal-to-string-conversion) Template literal to string conversion

**Mode:** `--minify-syntax`
Converts simple template literals to regular strings.

Input

Copy

```
`Hello World`
`Line 1
Line 2`
```

Output

Copy

```
"Hello World"
"Line 1\nLine 2"
```

### [​](https://bun.com/docs/bundler/minifier#string-quote-optimization) String quote optimization

**Mode:** `--minify-syntax`
Chooses the optimal quote character to minimize escapes.

Input

Copy

```
"It's a string"
'He said "hello"'
`Simple string`
```

Output

Copy

```
"It's a string"
'He said "hello"'
"Simple string"
```

### [​](https://bun.com/docs/bundler/minifier#array-spread-inlining) Array spread inlining

**Mode:** `--minify-syntax`
Inlines array spread operations with constant arrays.

Input

Copy

```
[1, ...[2, 3], 4]
[...[a, b]]
```

Output

Copy

```
[1,2,3,4]
[a,b]
```

### [​](https://bun.com/docs/bundler/minifier#array-indexing) Array indexing

**Mode:** `--minify-syntax`
Evaluates constant array access at compile time.

Input

Copy

```
[x][0]
['a', 'b', 'c'][1]
['a', , 'c'][1]
```

Output

Copy

```
x
'b'
void 0
```

### [​](https://bun.com/docs/bundler/minifier#property-access-optimization) Property access optimization

**Mode:** `--minify-syntax`
Converts bracket notation to dot notation when possible.

Input

Copy

```
obj["property"]
obj["validName"]
obj["123"]
obj["invalid-name"]
```

Output

Copy

```
obj.property
obj.validName
obj["123"]
obj["invalid-name"]
```

### [​](https://bun.com/docs/bundler/minifier#comparison-folding) Comparison folding

**Mode:** `--minify-syntax`
Evaluates constant comparisons at compile time.

Input

Copy

```
3 < 5
5 > 3
3 <= 3
5 >= 6
"a" < "b"
```

Output

Copy

```
!0
!0
!0
!1
!0
```

### [​](https://bun.com/docs/bundler/minifier#logical-operation-folding) Logical operation folding

**Mode:** `--minify-syntax`
Simplifies logical operations with constant values.

Input

Copy

```
true && x
false && x
true || x
false || x
```

Output

Copy

```
x
!1
!0
x
```

### [​](https://bun.com/docs/bundler/minifier#nullish-coalescing-folding) Nullish coalescing folding

**Mode:** `--minify-syntax`
Evaluates nullish coalescing with known values.

Input

Copy

```
null ?? x
undefined ?? x
42 ?? x
```

Output

Copy

```
x
x
42
```

### [​](https://bun.com/docs/bundler/minifier#comma-expression-simplification) Comma expression simplification

**Mode:** `--minify-syntax`
Removes side-effect-free expressions from comma sequences.

Input

Copy

```
(0, x)
(123, "str", x)
```

Output

Copy

```
x
x
```

### [​](https://bun.com/docs/bundler/minifier#ternary-conditional-folding) Ternary conditional folding

**Mode:** `--minify-syntax`
Evaluates conditional expressions with constant conditions.

Input

Copy

```
true ? a : b
false ? a : b
x ? true : false
x ? false : true
```

Output

Copy

```
a
b
x ? !0 : !1
x ? !1 : !0
```

### [​](https://bun.com/docs/bundler/minifier#unary-expression-folding) Unary expression folding

**Mode:** `--minify-syntax`
Simplifies unary operations.

Input

Copy

```
+123
+"123"
-(-x)
~~x
!!x
```

Output

Copy

```
123
123
123
123
x
~~x
!!x
x
```

### [​](https://bun.com/docs/bundler/minifier#double-negation-removal) Double negation removal

**Mode:** `--minify-syntax`
Removes unnecessary double negations.

Input

Copy

```
!!x
!!!x
```

Output

Copy

```
x
!x
```

### [​](https://bun.com/docs/bundler/minifier#if-statement-optimization) If statement optimization

**Mode:** `--minify-syntax`
Optimizes if statements with constant conditions.

Input

Copy

```
if (true) x;
if (false) x;
if (x) { a; }
if (x) {} else y;
```

Output

Copy

```
x;
// removed
if(x)a;
if(!x)y;
```

### [​](https://bun.com/docs/bundler/minifier#dead-code-elimination) Dead code elimination

**Mode:** `--minify-syntax`
Removes unreachable code and code without side effects.

Input

Copy

```
if (false) {
  unreachable();
}
function foo() {
  return x;
  deadCode();
}
```

Output

Copy

```
function foo(){return x}
```

### [​](https://bun.com/docs/bundler/minifier#unreachable-branch-removal) Unreachable branch removal

**Mode:** `--minify-syntax`
Removes branches that can never execute.

Input

Copy

```
while (false) {
  neverRuns();
}
```

Output

Copy

```
// removed entirely
```

### [​](https://bun.com/docs/bundler/minifier#empty-block-removal) Empty block removal

**Mode:** `--minify-syntax`
Removes empty blocks and unnecessary braces.

Input

Copy

```
{ }
if (x) { }
```

Output

Copy

```
;
// removed
```

### [​](https://bun.com/docs/bundler/minifier#single-statement-block-unwrapping) Single statement block unwrapping

**Mode:** `--minify-syntax`
Removes unnecessary braces around single statements.

Input

Copy

```
if (condition) {
  doSomething();
}
```

Output

Copy

```
if(condition)doSomething();
```

### [​](https://bun.com/docs/bundler/minifier#typescript-enum-inlining) TypeScript enum inlining

**Mode:** `--minify-syntax`
Inlines TypeScript enum values at compile time.

Input

Copy

```
enum Color { Red, Green, Blue }
const x = Color.Red;
```

Output

Copy

```
const x=0;
```

### [​](https://bun.com/docs/bundler/minifier#pure-annotation-support) Pure annotation support

**Mode:** Always active
Respects `/*@__PURE__*/` annotations for tree shaking.

Input

Copy

```
const x = /*@__PURE__*/ expensive();
// If x is unused...
```

Output

Copy

```
// removed entirely
```

### [​](https://bun.com/docs/bundler/minifier#identifier-renaming) Identifier renaming

**Mode:** `--minify-identifiers`
Renames local variables to shorter names based on usage frequency.

Input

Copy

```
function calculateSum(firstNumber, secondNumber) {
  const result = firstNumber + secondNumber;
  return result;
}
```

Output

Copy

```
function a(b,c){const d=b+c;return d}
```

**Naming strategy:**

* Most frequently used identifiers get the shortest names (a, b, c…)
* Single letters: a-z (26 names)
* Double letters: aa-zz (676 names)
* Triple letters and beyond as needed

**Preserved identifiers:**

* JavaScript keywords and reserved words
* Global identifiers
* Named exports (to maintain API)
* CommonJS names: `exports`, `module`

### [​](https://bun.com/docs/bundler/minifier#whitespace-removal) Whitespace removal

**Mode:** `--minify-whitespace`
Removes all unnecessary whitespace.

Input

Copy

```
function add(a, b) {
    return a + b;
}
let x = 10;
```

Output

Copy

```
function add(a,b){return a+b;}let x=10;
```

### [​](https://bun.com/docs/bundler/minifier#semicolon-optimization) Semicolon optimization

**Mode:** `--minify-whitespace`
Inserts semicolons only when necessary.

Input

Copy

```
let a = 1;
let b = 2;
return a + b;
```

Output

Copy

```
let a=1;let b=2;return a+b
```

### [​](https://bun.com/docs/bundler/minifier#operator-spacing-removal) Operator spacing removal

**Mode:** `--minify-whitespace`
Removes spaces around operators.

Input

Copy

```
a + b
x = y * z
foo && bar || baz
```

Output

Copy

```
a+b
x=y*z
foo&&bar||baz
```

### [​](https://bun.com/docs/bundler/minifier#comment-removal) Comment removal

**Mode:** `--minify-whitespace`
Removes comments except important license comments.

Input

Copy

```
// This comment is removed
/* So is this */
/*! But this license comment is kept */
function test() { /* inline comment */ }
```

Output

Copy

```
/*! But this license comment is kept */
function test(){}
```

### [​](https://bun.com/docs/bundler/minifier#object-and-array-formatting) Object and array formatting

**Mode:** `--minify-whitespace`
Removes whitespace in object and array literals.

Input

Copy

```
const obj = {
    name: "John",
    age: 30
};
const arr = [1, 2, 3];
```

Output

Copy

```
const obj={name:"John",age:30};const arr=[1,2,3];
```

### [​](https://bun.com/docs/bundler/minifier#control-flow-formatting) Control flow formatting

**Mode:** `--minify-whitespace`
Removes whitespace in control structures.

Input

Copy

```
if (condition) {
    doSomething();
}
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

Output

Copy

```
if(condition)doSomething();for(let i=0;i<10;i++)console.log(i);
```

### [​](https://bun.com/docs/bundler/minifier#function-formatting) Function formatting

**Mode:** `--minify-whitespace`
Removes whitespace in function declarations.

Input

Copy

```
function myFunction(param1, param2) {
    return param1 + param2;
}
const arrow = (a, b) => a + b;
```

Output

Copy

```
function myFunction(a,b){return a+b}const arrow=(a,b)=>a+b;
```

### [​](https://bun.com/docs/bundler/minifier#parentheses-minimization) Parentheses minimization

**Mode:** Always active
Only adds parentheses when necessary for operator precedence.

Input

Copy

```
(a + b) * c
a + (b * c)
((x))
```

Output

Copy

```
(a+b)*c
a+b*c
x
```

### [​](https://bun.com/docs/bundler/minifier#property-mangling) Property mangling

**Mode:** `--minify-identifiers` (with configuration)
Renames object properties to shorter names when configured.

Input

Copy

```
obj.longPropertyName
```

Output (with property mangling enabled)

Copy

```
obj.a
```

### [​](https://bun.com/docs/bundler/minifier#template-literal-value-folding) Template literal value folding

**Mode:** `--minify-syntax`
Converts non-string interpolated values to strings and folds them into the template.

Input

Copy

```
`hello ${123}`
`value: ${true}`
`result: ${null}`
`status: ${undefined}`
`big: ${10n}`
```

Output

Copy

```
"hello 123"
"value: true"
"result: null"
"status: undefined"
"big: 10"
```

### [​](https://bun.com/docs/bundler/minifier#string-length-constant-folding) String length constant folding

**Mode:** `--minify-syntax`
Evaluates `.length` property on string literals at compile time.

Input

Copy

```
"hello world".length
"test".length
```

Output

Copy

```
11
4
```

### [​](https://bun.com/docs/bundler/minifier#constructor-call-simplification) Constructor call simplification

**Mode:** `--minify-syntax`
Simplifies constructor calls for built-in types.

Input

Copy

```
new Object()
new Object(null)
new Object({a: 1})
new Array()
new Array(x, y)
```

Output

Copy

```
{}
{}
{a:1}
[]
[x,y]
```

### [​](https://bun.com/docs/bundler/minifier#single-property-object-inlining) Single property object inlining

**Mode:** `--minify-syntax`
Inlines property access for objects with a single property.

Input

Copy

```
({fn: () => console.log('hi')}).fn()
```

Output

Copy

```
(() => console.log('hi'))()
```

### [​](https://bun.com/docs/bundler/minifier#string-charcodeat-constant-folding) String charCodeAt constant folding

**Mode:** Always active
Evaluates `charCodeAt()` on string literals for ASCII characters.

Input

Copy

```
"hello".charCodeAt(1)
"A".charCodeAt(0)
```

Output

Copy

```
101
65
```

### [​](https://bun.com/docs/bundler/minifier#void-0-equality-to-null-equality) Void 0 equality to null equality

**Mode:** `--minify-syntax`
Converts loose equality checks with `void 0` to `null` since they’re equivalent.

Input

Copy

```
x == void 0
x != void 0
```

Output

Copy

```
x == null
x != null
```

### [​](https://bun.com/docs/bundler/minifier#negation-operator-optimization) Negation operator optimization

**Mode:** `--minify-syntax`
Moves negation operator through comma expressions.

Input

Copy

```
-(a, b)
-(x, y, z)
```

Output

Copy

```
a,-b
x,y,-z
```

### [​](https://bun.com/docs/bundler/minifier#import-meta-property-inlining) Import.meta property inlining

**Mode:** Bundle mode
Inlines `import.meta` properties at build time when values are known.

Input

Copy

```
import.meta.dir
import.meta.file
import.meta.path
import.meta.url
```

Output

Copy

```
"/path/to/directory"
"filename.js"
"/full/path/to/file.js"
"file:///full/path/to/file.js"
```

### [​](https://bun.com/docs/bundler/minifier#variable-declaration-merging) Variable declaration merging

**Mode:** `--minify-syntax`
Merges adjacent variable declarations of the same type.

Input

Copy

```
let a = 1;
let b = 2;
const c = 3;
const d = 4;
```

Output

Copy

```
let a=1,b=2;
const c=3,d=4;
```

### [​](https://bun.com/docs/bundler/minifier#expression-statement-merging) Expression statement merging

**Mode:** `--minify-syntax`
Merges adjacent expression statements using comma operator.

Input

Copy

```
console.log(1);
console.log(2);
console.log(3);
```

Output

Copy

```
console.log(1),console.log(2),console.log(3);
```

### [​](https://bun.com/docs/bundler/minifier#return-statement-merging) Return statement merging

**Mode:** `--minify-syntax`
Merges expressions before return with comma operator.

Input

Copy

```
console.log(x);
return y;
```

Output

Copy

```
return console.log(x),y;
```

### [​](https://bun.com/docs/bundler/minifier#throw-statement-merging) Throw statement merging

**Mode:** `--minify-syntax`
Merges expressions before throw with comma operator.

Input

Copy

```
console.log(x);
throw new Error();
```

Output

Copy

```
throw(console.log(x),new Error());
```

### [​](https://bun.com/docs/bundler/minifier#typescript-enum-cross-module-inlining) TypeScript enum cross-module inlining

**Mode:** `--minify-syntax` (bundle mode)
Inlines enum values across module boundaries.

Input

Copy

```
// lib.ts
export enum Color { Red, Green, Blue }

// Input (main.ts)
import { Color } from './lib';
const x = Color.Red;
```

Output

Copy

```
const x=0;
```

### [​](https://bun.com/docs/bundler/minifier#computed-property-enum-inlining) Computed property enum inlining

**Mode:** `--minify-syntax`
Inlines enum values used as computed object properties.

Input

Copy

```
enum Keys { FOO = 'foo' }
const obj = { [Keys.FOO]: value }
```

Output

Copy

```
const obj={foo:value}
```

### [​](https://bun.com/docs/bundler/minifier#string-number-to-numeric-index) String number to numeric index

**Mode:** `--minify-syntax`
Converts string numeric property access to numeric index.

Input

Copy

```
obj["0"]
arr["5"]
```

Output

Copy

```
obj[0]
arr[5]
```

### [​](https://bun.com/docs/bundler/minifier#arrow-function-body-shortening) Arrow function body shortening

**Mode:** Always active
Uses expression body syntax when an arrow function only returns a value.

Input

Copy

```
() => { return x; }
(a) => { return a + 1; }
```

Output

Copy

```
() => x
a => a + 1
```

### [​](https://bun.com/docs/bundler/minifier#object-property-shorthand) Object property shorthand

**Mode:** Always active
Uses shorthand syntax when property name and value identifier match.

Input

Copy

```
{ x: x, y: y }
{ name: name, age: age }
```

Output

Copy

```
{ x, y }
{ name, age }
```

### [​](https://bun.com/docs/bundler/minifier#method-shorthand) Method shorthand

**Mode:** Always active
Uses method shorthand syntax in object literals.

Input

Copy

```
{
  foo: function() {},
  bar: async function() {}
}
```

Output

Copy

```
{
  foo() {},
  async bar() {}
}
```

### [​](https://bun.com/docs/bundler/minifier#drop-debugger-statements) Drop debugger statements

**Mode:** `--drop=debugger`
Removes `debugger` statements from code.

Input

Copy

```
function test() {
  debugger;
  return x;
}
```

Output

Copy

```
function test(){return x}
```

### [​](https://bun.com/docs/bundler/minifier#drop-console-calls) Drop console calls

**Mode:** `--drop=console`
Removes all `console.*` method calls from code.

Input

Copy

```
console.log("debug");
console.warn("warning");
x = console.error("error");
```

Output

Copy

```
void 0;
void 0;
x=void 0;
```

### [​](https://bun.com/docs/bundler/minifier#drop-custom-function-calls) Drop custom function calls

**Mode:** `--drop=<name>`
Removes calls to specified global functions or methods.

Input

Copy

```
assert(condition);
obj.assert(test);
```

Output with --drop=assert

Copy

```
void 0;
void 0;
```

## [​](https://bun.com/docs/bundler/minifier#keep-names) Keep Names

When minifying identifiers, you may want to preserve original function and class names for debugging purposes. Use the `--keep-names` flag:

Copy

```
bun build ./index.ts --minify --keep-names --outfile=out.js
```

Or in the JavaScript API:

Copy

```
await Bun.build({
  entrypoints: ["./index.ts"],
  outdir: "./out",
  minify: {
    identifiers: true,
    keepNames: true,
  },
});
```

This preserves the `.name` property on functions and classes while still minifying the actual identifier names in the code.

## [​](https://bun.com/docs/bundler/minifier#combined-example) Combined Example

Using all three minification modes together:

input.ts (158 bytes)

Copy

```
const myVariable = 42;

const myFunction = () => {
  const isValid = true;
  const result = undefined;
  return isValid ? myVariable : result;
};

const output = myFunction();
```

output.js

Copy

```
// Output with --minify (49 bytes, 69% reduction)
const a=42,b=()=>{const c=!0,d=void 0;return c?a:d},e=b();
```

## [​](https://bun.com/docs/bundler/minifier#when-to-use-minification) When to Use Minification

**Use `--minify` for:**

* Production bundles
* Reducing CDN bandwidth costs
* Improving page load times

**Use individual modes for:**

* **`--minify-whitespace`:** Quick size reduction without semantic changes
* **`--minify-syntax`:** Smaller output while keeping readable identifiers for debugging
* **`--minify-identifiers`:** Maximum size reduction (combine with `--keep-names` for better stack traces)

**Avoid minification for:**

* Development builds (harder to debug)
* When you need readable error messages
* Libraries where consumers may read the source

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/bundler/minifier.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /bundler/minifier)

⌘I