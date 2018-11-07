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

当使用严格模式时，任何 `assert` 函数都会使用严格函数模式的等式。
所以 [`assert.deepEqual()`] 会等同于 [`assert.deepStrictEqual()`]。

除此以外，涉及对象的错误信息会产生一个错误差异比较，而不是展示双方的对象。
遗留模式则不会这样。

可以通过以下方式使用：

```js
const assert = require('assert').strict;
```

错误差异比较的例子：

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

使用 `NODE_DISABLE_COLORS` 环境变量可以禁用颜色。
但这也会禁用 REPL 中的其他颜色。

