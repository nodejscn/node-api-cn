<!-- YAML
added: v0.3.1
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19016
    description: The `contextCodeGeneration` option is supported now.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6635
    description: The `breakOnSigint` option is supported now.
-->

* `contextObject` {Object} 一个将会被[上下文隔离化][contextified]的对象。如果是 `undefined`, 则会生成一个新的对象。
* `options` {Object}
  * `displayErrors` {boolean} 当值为 `true` 的时候，假如在解析代码的时候发生错误 [`Error`][]，引起错误的行将会被加入堆栈跟踪信息。**默认值:** `true`。
  * `timeout` {integer} 定义在被终止执行之前此 `code` 被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误 [`Error`][]。该值必须是严格正整数。
  * `breakOnSigint` {boolean} 若值为 `true`，当收到 `SIGINT` (Ctrl+C)事件时，代码会被终止执行。
     此外，通过 `process.on('SIGINT')` 方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。如果执行被终止，一个错误 [`Error`][] 会被抛出。**默认值:** `false`。
  * `contextName` {string} 新创建的上下文的人类可读名称。 **默认值:** `'VM Context i'`，其中 `i` 是创建的上下文的升序数字索引。
  * `contextOrigin` {string} 对应于新创建用于显示目的的上下文的[原点][origin]。 
    原点应格式化为类似一个 URL，但只包含协议，主机和端口（如果需要），例如 [`URL`] 对象的 [`url.origin`] 属性的值。 最值得注意的是，此字符串应省略尾部斜杠，因为它表示路径。 **默认值:** `''`。
  * `contextCodeGeneration` {Object}
    * `strings` {boolean} 如果设置为 `false`，则对 `eval` 或函数构造函数（`Function`、`GeneratorFunction` 等）的任何调用都将抛出 `EvalError`。**默认值:** `true`。
    * `wasm` {boolean} 如果设置为 `false`，则任何编译 WebAssembly 模块的尝试都将抛出 `WebAssembly.CompileError`。**默认值:** `true`。
* 返回: {any} 脚本中执行的最后一个语句的结果。

首先给指定的 `contextObject` 提供一个隔离的上下文, 再在此上下文中执行 `vm.Script` 中被编译的代码，最后返回结果。运行中的代码无法获取本地作用域。

以下的例子会编译一段代码，该代码会递增一个全局变量，给另外一个全局变量赋值。同时该代码被编译后会被多次执行。全局变量会被置于各个独立的 `context` 对象内。

```js
const util = require('util');
const vm = require('vm');

const script = new vm.Script('globalVar = "set"');

const contexts = [{}, {}, {}];
contexts.forEach((context) => {
  script.runInNewContext(context);
});

console.log(contexts);
// 打印: [{ globalVar: 'set' }, { globalVar: 'set' }, { globalVar: 'set' }]
```

