<!-- YAML
added: v0.3.1
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19398
    description: The first argument can no longer be a function.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19016
    description: The `codeGeneration` option is supported now.
-->

* `contextObject` {Object}
* `options` {Object}
  * `name` {string} 新创建的上下文的人类可读名称。 **默认值:** `'VM Context i'`，其中 `i` 是创建的上下文的升序数字索引。
  * `origin` {string} 对应于新创建用于显示目的的上下文的[原点][origin]。 
    原点应格式化为类似一个 URL，但只包含协议，主机和端口（如果需要），例如 [`URL`] 对象的 [`url.origin`] 属性的值。 最值得注意的是，此字符串应省略尾部斜杠，因为它表示路径。 **默认值:** `''`。
  * `codeGeneration` {Object}
    * `strings` {boolean} 如果设置为 `false`，则对 `eval` 或函数构造函数（`Function`、`GeneratorFunction` 等）的任何调用都将抛出 `EvalError`。**默认值:** `true`。
    * `wasm` {boolean} 如果设置为 `false`，则任何编译 WebAssembly 模块的尝试都将抛出 `WebAssembly.CompileError`。**默认值:** `true`。
* 返回: {Object} 上下文隔离化的沙盒。

给定一个 `contextObject` 对象，`vm.createContext()` 会[设置此沙盒][contextified]，从而让它具备在 [`vm.runInContext()`][] 或者 [`script.runInContext()`][] 中被使用的能力。
在此类脚本中，`contextObject` 将会是全局对象，保留其所有现有属性，但还具有任何标准的[全局对象][global object]具有的内置对象和函数。 
在 `vm` 模块运行的脚本之外，全局变量将会保持不变。


```js
const util = require('util');
const vm = require('vm');

global.globalVar = 3;

const context = { globalVar: 1 };
vm.createContext(context);

vm.runInContext('globalVar *= 2;', context);

console.log(util.inspect(context)); // { globalVar: 2 }

console.log(util.inspect(globalVar)); // 3
```

如果未提供 `contextObject`（或者传入`undefined`），那么会返回一个全新的空的[上下文隔离化][contextified]对象。

`vm.createContext()` 主要是用于创建一个能运行多个脚本的上下文。
比如说，在模拟一个网页浏览器时，此方法可以被用于创建一个单独的上下文来代表一个窗口的全局对象，然后所有的 `<script>` 标签都可以在这个上下文中运行。

通过 Inspector API 可以看到提供的上下文的 `name` 和 `origin`。

