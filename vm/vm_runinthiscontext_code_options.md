<!-- YAML
added: v0.3.1
-->

* `code` {string} 将被编译和运行的JavaScript代码
* `options`
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误Error，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[`Error`][]

`vm.runInThisContext()`在当前的`global`对象的上下文中编译并执行`code`，最后返回结果。运行中的代码无法获取本地作用域，但可以获取当前的`global`对象。

下面的例子演示了使用`vm.runInThisContext()`和JavaScript的[`eval()`][]方法去执行相同的一段代码：

<!-- eslint-disable prefer-const -->
```js
const vm = require('vm');
let localVar = 'initial value';

const vmResult = vm.runInThisContext('localVar = "vm";');
console.log('vmResult:', vmResult);
console.log('localVar:', localVar);

const evalResult = eval('localVar = "eval";');
console.log('evalResult:', evalResult);
console.log('localVar:', localVar);

// vmResult: 'vm', localVar: 'initial value'
// evalResult: 'eval', localVar: 'eval'
```

正因`vm.runInThisContext()`无法获取本地作用域，故`localVar`的值不变。相反，[`eval()`]*确实*能获取本地作用域，所以`localVar`的值被改变了。如此看来，`vm.runInThisContext()`更像是[间接的执行`eval()`][indirect `eval()` call], 就像`(0, eval)('code')`

