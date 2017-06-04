<!-- YAML
added: v0.3.0
changes:
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

* `object` {any} 任何 JavaScript 原始值或对象。
* `options` {Object}
  * `showHidden` {boolean} 如果为 `true`，则 `object` 的不可枚举的符号与属性也会被包括在格式化后的结果中。
    默认为 `false`。
  * `depth` {number} 指定格式化 `object` 时递归的次数。
    这对查看大型复杂对象很有用。
    默认为 `2`。
    若要无限地递归则传入 `null`。
  * `colors` {boolean} 如果为 `true`，则输出样式使用 ANSI 颜色代码。
    默认为 `false`。
    颜色可自定义，详见[自定义 `util.inspect` 颜色]。
  * `customInspect` {boolean} 如果为 `false`，则 `object` 上自定义的 `inspect(depth, opts)` 函数不会被调用。
    默认为 `true`。
  * `showProxy` {boolean} 如果为 `true`，则 `Proxy` 对象的对象和函数会展示它们的 `target` 和 `handler` 对象。
    默认为 `false`。
  * `maxArrayLength` {number} 指定格式化时数组和 `TypedArray` 元素能包含的最大数量。
    默认为 `100`。
    设为 `null` 则显式全部数组元素。
    设为 `0` 或负数则不显式数组元素。
  * `breakLength` {number} 一个对象的键被拆分成多行的长度。
    设为 `Infinity` 则格式化一个对象为单行。
    默认为 `60`。

`util.inspect()` 方法返回 `object` 的字符串表示，主要用于调试。
附加的 `options` 可用于改变格式化字符串的某些方面。

例子，查看 `util` 对象的所有属性：

```js
const util = require('util');

console.log(util.inspect(util, { showHidden: true, depth: null }));
```

当调用到达递归查看的当前 `depth` 时，值支持自定义的 `inspect(depth, opts)` 函数，传入 `util.inspect()` 的选项对象也一样。

