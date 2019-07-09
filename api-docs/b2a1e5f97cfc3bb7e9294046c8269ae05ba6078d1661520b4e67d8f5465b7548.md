<!-- YAML
added: v0.3.1
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19398
    description: The `sandbox` option can no longer be a function.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19016
    description: The `codeGeneration` option is supported now.
-->

* `sandbox` {Object}
* `options` {Object}
  * `name` {string} 阅读友好的新创建的上下文名字。
    **默认:** `'VM Context i'`，其中 `i` 是创建的上下文的递增数字索引。
  * `origin` {string} [Origin][origin] 相当于新创建的用于展示的上下文。	
    Origin 的格式就想一个 URL，但只有协议、主机和端口（如果需要的话），就像 [`URL`][] 对象的 [`url.origin`][] 属性。	
    尤其需要注意的是，origin 字符串需要去掉尾部的斜杠，因为它表示一个路径。**默认:** `''`。
  * `codeGeneration` {Object}
    * `strings` {boolean} 如果设置为 false，则调用 `eval` 或构造函数（`Function`、`GeneratorFunction` 等） 都将抛出 `EvalError` 错误。**默认:** `true`.
    * `wasm` {boolean} 如果设置为 false，则尝试编译 WebAssembly 模块将会抛出 `WebAssembly.CompileError` 错误。**默认:** `true`.
      

如果提供了 `sandbox` 对象，则 `vm.createContext()` 方法将会对沙盒进行预处理（[prepare
that sandbox][contextified]），所以它可以在调用 [`vm.runInContext()`][] or [`script.runInContext()`][] 的时候使用。在下面的脚本中，`sandbox` 对象将是全局对象，保留所有现有属性，并具有任何标准 [全局对象][] 所拥有的内置对象和函数。在 vm 模块运行的脚本外面，全局变量将保持不变。


```js
const util = require('util');
const vm = require('vm');

global.globalVar = 3;

const sandbox = { globalVar: 1 };
vm.createContext(sandbox);

vm.runInContext('globalVar *= 2;', sandbox);

console.log(util.inspect(sandbox)); // { globalVar: 2 }

console.log(util.inspect(globalVar)); // 3
```

如果省略了 `sandbox` （或显示传入 `undefined`），将返回一个新的、空的上下文隔离（[contextified][]）的沙盒对象。

`vm.createContext()` 方法的主要用于创建可以运行多个脚本的单个沙盒。例如，如果要模仿一个 Web 浏览器，则该方法可以用于创建表示 window 全局对象的单个沙盒，然后在该沙盒的上下文中一起运行所有 `<script>` 标签。


通过 Inspector API 可以看到给上下文提供的 `name` 和 `origin`。

