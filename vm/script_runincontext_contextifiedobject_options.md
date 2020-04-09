<!-- YAML
added: v0.3.1
changes:
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6635
    description: The `breakOnSigint` option is supported now.
-->

* `contextifiedObject` {Object} 由 `vm.createContext()` 返回的[上下文隔离化][contextified]的对象。
* `options` {Object}
  * `displayErrors` {boolean} 当值为 `true` 的时候，假如在解析代码的时候发生错误 [`Error`][]，引起错误的行将会被加入堆栈跟踪信息。**默认值:** `true`。
  * `timeout` {integer} 定义在被终止执行之前此 `code` 被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误 [`Error`][]。该值必须是严格正整数。
  * `breakOnSigint` {boolean} 若值为 `true`，当收到 `SIGINT` (Ctrl+C)事件时，代码会被终止执行。
     此外，通过 `process.on('SIGINT')` 方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。如果执行被终止，一个错误 [`Error`][] 会被抛出。**默认值:** `false`。
* 返回: {any} 脚本中执行的最后一个语句的结果。

在指定的 `contextifiedObject` 中执行 `vm.Script` 对象中被编译后的代码并返回其结果。被执行的代码无法获取本地作用域。

以下的例子会编译一段代码，该代码会递增一个全局变量，给另外一个全局变量赋值。同时该代码被编译后会被多次执行。全局变量会被置于 `context` 对象内。

```js
const util = require('util');
const vm = require('vm');

const context = {
  animal: 'cat',
  count: 2
};

const script = new vm.Script('count += 1; name = "kitty";');

vm.createContext(context);
for (let i = 0; i < 10; ++i) {
  script.runInContext(context);
}

console.log(context);
// 打印: { animal: 'cat', count: 12, name: 'kitty' }
```

使用 `timeout` 或者 `breakOnSigint` 选项会导致若干新的事件循环以及对应的线程，这有一个非零的性能消耗。
