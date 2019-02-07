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

当使用严格模式（`strict mode`）时，任何 `assert` 函数都将使用严格函数模式中使用的相等性。 
因此，[`assert.deepEqual()`] 将与 [`assert.deepStrictEqual()`] 一样效果。

最重要的是，涉及对象的错误消息将产生错误的差异，而不是显示两个对象。 
遗留模式则不是这种情况。

它可以使用以下方式访问：

```js
const assert = require('assert').strict;
```

错误差异的示例：

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

要停用颜色，则使用 `NODE_DISABLE_COLORS` 环境变量。 
注意，这也将停用 REPL 中的颜色。

