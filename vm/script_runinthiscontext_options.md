<!-- YAML
added: v0.3.1
-->
* `options` {Object}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误[`Error`][]，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[`Error`][]。

在指定的`global`对象的上下文中执行`vm.Script`对象里被编译的代码并返回其结果。被执行的代码虽然无法获取本地作用域，但是能获取`global`对象。

以下的例子会编译一段代码，该代码会递增一个`global`变量。同时该代码被编译后会被多次执行。

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

