<!-- YAML
added: v0.3.1
-->
* `options` {Object}
  * `displayErrors` {boolean} 当值为 `true` 的时候，假如在解析代码的时候发生错误 [`Error`][]，引起错误的行将会被加入堆栈跟踪信息。**默认值:** `true`。
  * `timeout` {integer} 定义在被终止执行之前此 `code` 被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误 [`Error`][]。该值必须是严格正整数。
  * `breakOnSigint` {boolean} 若值为 `true`，接收到 `SIGINT`（<kbd>Ctrl</kbd>+<kbd>C</kbd>）会终止执行并抛出 [`Error`]。
     通过 `process.on('SIGINT')` 方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。
     **默认值:** `false`。
* 返回: {any} 脚本中执行的最后一个语句的结果。

在指定的 `global` 对象的上下文中执行 `vm.Script` 对象里被编译的代码并返回其结果。被执行的代码虽然无法获取本地作用域，但是能获取 `global` 对象。

以下的例子会编译一段代码，该代码会递增一个 `global` 变量。同时该代码被编译后会被多次执行。

```js
const vm = require('vm');

global.globalVar = 0;

const script = new vm.Script('globalVar += 1', { filename: 'myfile.vm' });

for (let i = 0; i < 1000; ++i) {
  script.runInThisContext();
}

console.log(globalVar);

// 1000
```

