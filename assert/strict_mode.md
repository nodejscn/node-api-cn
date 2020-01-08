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

在严格模式中，任何 `assert` 函数都将使用严格函数模式中使用的相等性。 
例如，[`assert.deepEqual()`] 将与 [`assert.deepStrictEqual()`] 一样效果。

在严格模式中，对象的错误消息会显示差异。
在遗留模式下，对象的错误消息会显示对象，通常是截断的。

使用严格模式：

```js
const assert = require('assert').strict;
```

错误差异的示例：

```js
const assert = require('assert').strict;

assert.deepEqual([[[1, 2, 3]], 4, 5], [[[1, 2, '3']], 4, 5]);
// AssertionError: Expected inputs to be strictly deep-equal:
// + actual - expected ... Lines skipped
//
//   [
//     [
// ...
//       2,
// +     3
// -     '3'
//     ],
// ...
//     5
//   ]
```

要停用颜色，则使用 `NO_COLOR` 或 `NODE_DISABLE_COLORS` 环境变量。 
注意，这也将停用 REPL 中的颜色。

有关终端环境中颜色支持的更多信息，参阅 [getColorDepth()][_tty_writestream_getcolordepth] 文档。

