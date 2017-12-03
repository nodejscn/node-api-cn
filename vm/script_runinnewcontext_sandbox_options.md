<!-- YAML
added: v0.3.1
-->

* `sandbox` {Object} An object that will be [contextified][]. If `undefined`, a
  new object will be created. 一个将被[`contextified`][]的对象。如果是`undefined`, 会生成一个新的对象
* `options` {Object}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误[`Error`][]，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[`Error`][]。

首先给指定的`sandbox`提供一个隔离的上下文, 再在此上下文中执行`vm.Script`中被编译的代码，最后返回结果。运行中的代码无法获取本地作用域。

以下的例子会编译一段代码，该代码会递增一个全局变量，给另外一个全局变量赋值。同时该代码被编译后会被多次执行。全局变量会被置于各个独立的`sandbox`对象内。

```js
const util = require('util');
const vm = require('vm');

const script = new vm.Script('globalVar = "set"');

const sandboxes = [{}, {}, {}];
sandboxes.forEach((sandbox) => {
  script.runInNewContext(sandbox);
});

console.log(util.inspect(sandboxes));

// [{ globalVar: 'set' }, { globalVar: 'set' }, { globalVar: 'set' }]
```

