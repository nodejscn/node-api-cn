<!-- YAML
added: v0.1.21
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15001
    description: The `Error` names and messages are now properly compared
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12142
    description: The `Set` and `Map` content is also compared
  - version: v6.4.0, v4.7.1
    pr-url: https://github.com/nodejs/node/pull/8002
    description: Typed array slices are handled correctly now.
  - version: v6.1.0, v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6432
    description: Objects with circular references can be used as inputs now.
  - version: v5.10.1, v4.4.3
    pr-url: https://github.com/nodejs/node/pull/5910
    description: Handle non-`Uint8Array` typed arrays correctly.
-->
* `actual` {any}
* `expected` {any}
* `message` {string|Error}

**strict 模式**

[`assert.deepStrictEqual()`] 的别名。

**legacy 模式**

> 稳定性: 0 - 废弃的: 使用 [`assert.deepStrictEqual()`] 代替。

Tests for deep equality between the `actual` and `expected` parameters.
Primitive values are compared with the [Abstract Equality Comparison][]
( `==` ).

Only [enumerable "own" properties][] are considered. The
[`assert.deepEqual()`][] implementation does not test the
[`[[Prototype]]`][prototype-spec] of objects or enumerable own [`Symbol`][]
properties. For such checks, consider using [`assert.deepStrictEqual()`][]
instead. [`assert.deepEqual()`][] can have potentially surprising results. The
following example does not throw an `AssertionError` because the properties on
the [`RegExp`][] object are not enumerable:

```js
// WARNING: This does not throw an AssertionError!
assert.deepEqual(/a/gi, new Date());
```

An exception is made for [`Map`][] and [`Set`][]. `Map`s and `Set`s have their
contained items compared too, as expected.

"Deep" equality means that the enumerable "own" properties of child objects
are evaluated also:

```js
const assert = require('assert');

const obj1 = {
  a: {
    b: 1
  }
};
const obj2 = {
  a: {
    b: 2
  }
};
const obj3 = {
  a: {
    b: 1
  }
};
const obj4 = Object.create(obj1);

assert.deepEqual(obj1, obj1);
// OK

// Values of b are different:
assert.deepEqual(obj1, obj2);
// AssertionError: { a: { b: 1 } } deepEqual { a: { b: 2 } }

assert.deepEqual(obj1, obj3);
// OK

// Prototypes are ignored:
assert.deepEqual(obj1, obj4);
// AssertionError: { a: { b: 1 } } deepEqual {}
```

If the values are not equal, an `AssertionError` is thrown with a `message`
property set equal to the value of the `message` parameter. If the `message`
parameter is undefined, a default error message is assigned. If the `message`
parameter is an instance of an [`Error`][] then it will be thrown instead of the
`AssertionError`.

