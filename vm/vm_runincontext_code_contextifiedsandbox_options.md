
* `code` {string} 将被编译和运行的JavaScript代码
* `contextifiedSandbox` {Object} 一个被[上下文隔离化][contextified]过的对象，会在代码被编译和执行之后充当`global`对象
* `options`
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误[`Error`][]，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[`Error`][]

`vm.runInContext()`在指定的`contextifiedSandbox`的上下文里执行vm.Script对象中被编译后的代码并返回其结果。被执行的代码无法获取本地作用域。`contextifiedSandbox`*必须*是事先被[`vm.createContext()`][][上下文隔离化][contextified]过的对象。

以下例子使用一个单独的, [上下文隔离化][contextified]过的对象来编译并运行几个不同的脚本:

```js
const util = require('util');
const vm = require('vm');

const sandbox = { globalVar: 1 };
vm.createContext(sandbox);

for (let i = 0; i < 10; ++i) {
  vm.runInContext('globalVar *= 2;', sandbox);
}
console.log(util.inspect(sandbox));

// { globalVar: 1024 }
```

