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

当使用严格模式时，`assert` 方法会使用严格模式的等式。
例如 [`assert.deepEqual()`] 会等同于 [`assert.deepStrictEqual()`]。

除此以外，错误的信息会生成差异对比，而不只是展示对象。

使用方法如下：

```js
const assert = require('assert').strict;
```

例子，错误的差异对比：

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

