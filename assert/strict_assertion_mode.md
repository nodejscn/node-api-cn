<!-- YAML
added: v9.9.0
changes:
  - version: v12.16.2
    description: Changed "strict mode" to "strict assertion mode" and "legacy
                 mode" to "legacy assertion mode" to avoid confusion with the
                 more usual meaining of "strict mode".
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17615
    description: Added error diffs to the strict assertion mode.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17002
    description: Added strict assertion mode to the assert module.
-->

在严格的断言模式中，非严格的方法与它们对应的严格方法的行为是一样的。
例如，[`assert.deepEqual()`] 将与 [`assert.deepStrictEqual()`] 一样效果。

在严格的断言模式中，对象的错误消息会显示差异。
在遗留的断言模式下，对象的错误消息会显示对象，通常是截断的。

使用严格的断言模式：

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
这也将停用 REPL 中的颜色。
有关终端环境中颜色支持的更多信息，参阅 [getColorDepth()][_tty_writestream_getcolordepth] 文档。

