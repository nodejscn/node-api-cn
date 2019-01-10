<!-- YAML
added: v0.3.0
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/22788
    description: The `sorted` option is supported now.
  - version: v10.6.0
    pr-url: https://github.com/nodejs/node/pull/20725
    description: Inspecting linked lists and similar objects is now possible
                 up to the maximum call stack size.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19259
    description: The `WeakMap` and `WeakSet` entries can now be inspected.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17576
    description: The `compact` option is supported now.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8174
    description: Custom inspection functions can now return `this`.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/7499
    description: The `breakLength` option is supported now.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6334
    description: The `maxArrayLength` option is supported now; in particular,
                 long arrays are truncated by default.
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/6465
    description: The `showProxy` option is supported now.
-->

* `object` {any} Any JavaScript primitive or `Object`.
* `options` {Object}
  * `showHidden` {boolean} If `true`, the `object`'s non-enumerable symbols and
    properties will be included in the formatted result as well as [`WeakMap`][]
    and [`WeakSet`][] entries. **Default:** `false`.
  * `depth` {number} Specifies the number of times to recurse while formatting
    the `object`. This is useful for inspecting large complicated objects. To
    make it recurse up to the maximum call stack size pass `Infinity` or `null`.
    **Default:** `2`.
  * `colors` {boolean} If `true`, the output will be styled with ANSI color
    codes. Colors are customizable, see [Customizing `util.inspect` colors][].
    **Default:** `false`.
  * `customInspect` {boolean} If `false`, then custom `inspect(depth, opts)`
    functions will not be called. **Default:** `true`.
  * `showProxy` {boolean} If `true`, then objects and functions that are
    `Proxy` objects will be introspected to show their `target` and `handler`
    objects. **Default:** `false`.
    <!--
    TODO(BridgeAR): Deprecate `maxArrayLength` and replace it with
                    `maxEntries`.
    -->
  * `maxArrayLength` {number} Specifies the maximum number of `Array`,
    [`TypedArray`][], [`WeakMap`][] and [`WeakSet`][] elements to include when
    formatting. Set to `null` or `Infinity` to show all elements. Set to `0` or
    negative to show no elements. **Default:** `100`.
  * `breakLength` {number} The length at which an object's keys are split
    across multiple lines. Set to `Infinity` to format an object as a single
    line. **Default:** `60` for legacy compatibility.
  * `compact` {boolean} Setting this to `false` changes the default indentation
    to use a line break for each object key instead of lining up multiple
    properties in one line. It will also break text that is above the
    `breakLength` size into smaller and better readable chunks and indents
    objects the same as arrays. Note that no text will be reduced below 16
    characters, no matter the `breakLength` size. For more information, see the
    example below. **Default:** `true`.
  * `sorted` {boolean|Function} If set to `true` or a function, all properties
    of an object and Set and Map entries will be sorted in the returned string.
    If set to `true` the [default sort][] is going to be used. If set to a
    function, it is used as a [compare function][].
* Returns: {string} The representation of passed object

The `util.inspect()` method returns a string representation of `object` that is
intended for debugging. The output of `util.inspect` may change at any time
and should not be depended upon programmatically. Additional `options` may be
passed that alter certain aspects of the formatted string.
`util.inspect()` will use the constructor's name and/or `@@toStringTag` to make
an identifiable tag for an inspected value.

```js
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

The following example inspects all properties of the `util` object:

```js
const util = require('util');

console.log(util.inspect(util, { showHidden: true, depth: null }));
```

Values may supply their own custom `inspect(depth, opts)` functions, when
called these receive the current `depth` in the recursive inspection, as well as
the options object passed to `util.inspect()`.

The following example highlights the difference with the `compact` option:

```js
const util = require('util');

const o = {
  a: [1, 2, [[
    'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do ' +
      'eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    'test',
    'foo']], 4],
  b: new Map([['za', 1], ['zb', 'test']])
};
console.log(util.inspect(o, { compact: true, depth: 5, breakLength: 80 }));

// This will print

// { a:
//   [ 1,
//     2,
//     [ [ 'Lorem ipsum dolor sit amet, consectetur [...]', // A long line
//           'test',
//           'foo' ] ],
//     4 ],
//   b: Map { 'za' => 1, 'zb' => 'test' } }

// Setting `compact` to false changes the output to be more reader friendly.
console.log(util.inspect(o, { compact: false, depth: 5, breakLength: 80 }));

// {
//   a: [
//     1,
//     2,
//     [
//       [
//         'Lorem ipsum dolor sit amet, consectetur ' +
//           'adipiscing elit, sed do eiusmod tempor ' +
//           'incididunt ut labore et dolore magna ' +
//           'aliqua.,
//         'test',
//         'foo'
//       ]
//     ],
//     4
//   ],
//   b: Map {
//     'za' => 1,
//     'zb' => 'test'
//   }
// }

// Setting `breakLength` to e.g. 150 will print the "Lorem ipsum" text in a
// single line.
// Reducing the `breakLength` will split the "Lorem ipsum" text in smaller
// chunks.
```

Using the `showHidden` option allows to inspect [`WeakMap`][] and [`WeakSet`][]
entries. If there are more entries than `maxArrayLength`, there is no guarantee
which entries are displayed. That means retrieving the same [`WeakSet`][]
entries twice might actually result in a different output. Besides this any item
might be collected at any point of time by the garbage collector if there is no
strong reference left to that object. Therefore there is no guarantee to get a
reliable output.

```js
const { inspect } = require('util');

const obj = { a: 1 };
const obj2 = { b: 2 };
const weakSet = new WeakSet([obj, obj2]);

console.log(inspect(weakSet, { showHidden: true }));
// WeakSet { { a: 1 }, { b: 2 } }
```

The `sorted` option makes sure the output is identical, no matter of the
properties insertion order:

```js
const { inspect } = require('util');
const assert = require('assert');

const o1 = {
  b: [2, 3, 1],
  a: '`a` comes before `b`',
  c: new Set([2, 3, 1])
};
console.log(inspect(o1, { sorted: true }));
// { a: '`a` comes before `b`', b: [ 2, 3, 1 ], c: Set { 1, 2, 3 } }
console.log(inspect(o1, { sorted: (a, b) => b.localeCompare(a) }));
// { c: Set { 3, 2, 1 }, b: [ 2, 3, 1 ], a: '`a` comes before `b`' }

const o2 = {
  c: new Set([2, 1, 3]),
  a: '`a` comes before `b`',
  b: [2, 3, 1]
};
assert.strict.equal(
  inspect(o1, { sorted: true }),
  inspect(o2, { sorted: true })
);
```

Please note that `util.inspect()` is a synchronous method that is mainly
intended as a debugging tool. Some input values can have a significant
performance overhead that can block the event loop. Use this function
with care and never in a hot code path.

