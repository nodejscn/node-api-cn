<!-- YAML
added: v9.9.0
changes:
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17615
    description: Added error diffs to the strict mode
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17002
    description: Added strict mode to the assert module.
-->

When using the `strict mode`, any `assert` function will use the equality used
in the strict function mode. So [`assert.deepEqual()`][] will, for example,
work the same as [`assert.deepStrictEqual()`][].

On top of that, error messages which involve objects produce an error diff
instead of displaying both objects. That is not the case for the legacy mode.

It can be accessed using:

```js
const assert = require('assert').strict;
```

Example error diff:

```js
const assert = require('assert').strict;

assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
// AssertionError: Input A expected to strictly deep-equal input B:
// + expected - actual ... Lines skipped
//
//   [
//     [
// ...
//       2,
// -     3
// +     '3'
//     ],
// ...
//     5
//   ]
```

To deactivate the colors, use the `NODE_DISABLE_COLORS` environment variable.
Please note that this will also deactivate the colors in the REPL.

