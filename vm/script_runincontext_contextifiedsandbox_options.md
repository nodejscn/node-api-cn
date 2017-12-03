<!-- YAML
added: v0.3.1
changes:
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6635
    description: 现已支持`breakOnSigint`选项。
-->

* `contextifiedSandbox` {Object} 由`vm.createContext()`返回的[`contextified`][]对象
* `options` {Object}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误[`Error`][]，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[`Error`][]。
  * `breakOnSigint`: 若值为真，当收到`SIGINT` (Ctrl+C)事件时，代码会被终止执行。此外，通过`process.on("SIGINT")`方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。如果执行被终止，一个错误[`Error`][]会被抛出。

在指定的`contextifiedSandbox`中执行`vm.Script`对象中被编译后的代码并返回其结果。被执行的代码无法获取本地作用域。

以下的例子会编译一段代码，该代码会递增一个全局变量，给另外一个全局变量赋值。同时该代码被编译后会被多次执行。全局变量会被置于`sandbox`对象内。

```js
const util = require('util');
const vm = require('vm');

const sandbox = {
  animal: 'cat',
  count: 2
};

const script = new vm.Script('count += 1; name = "kitty";');

const context = vm.createContext(sandbox);
for (let i = 0; i < 10; ++i) {
  script.runInContext(context);
}

console.log(util.inspect(sandbox));

// { animal: 'cat', count: 12, name: 'kitty' }
```

*注意*: 使用`timeout`或者`breakOnSigint`选项会导致若干新的事件循环以及对应的线程，这有一个非零的性能消耗。
