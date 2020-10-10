<!-- YAML
added: v9.9.0
changes:
  - version:
      - v13.9.0
      - v12.16.2
    description: 将“严格模式”更改为“严格的断言模式”，将“传统模式”更改为“传统的断言模式”，以避免与更常见的“严格模式”的含义混淆。
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17615
    description: 添加错误差异到严格的断言模式。
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/17002
    description: 添加严格的断言模式到断言模块。
-->

在严格的断言模式中，非严格方法的行为类似于其对应的严格方法。
例如，[`assert.deepEqual()`] 的行为类似于 [`assert.deepStrictEqual()`]。

在严格的断言模式中，对象的错误消息会显示差异。
在传统的断言模式中，对象的错误消息会显示对象（通常是截断的）。

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

若要禁用颜色，则使用 `NO_COLOR` 或 `NODE_DISABLE_COLORS` 环境变量。 
这也会禁用 REPL 中的颜色。
有关终端环境中的颜色支持，详见 tty 的 [getColorDepth()][_tty_writestream_getcolordepth] 文档。

