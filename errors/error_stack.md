
* {string}

`error.stack` 属性是一个字符串，描述代码中 `Error` 被实例化的位置。

例子：

```txt
Error: Things keep happening!
   at /home/gbusey/file.js:525:2
   at Frobnicator.refrobulate (/home/gbusey/business-logic.js:424:21)
   at Actor.<anonymous> (/home/gbusey/actors.js:400:8)
   at increaseSynergy (/home/gbusey/actors.js:701:6)
```

第一行会被格式化为 `<error class name>: <error message>`，且带上一系列栈帧（每一行都以 "at " 开头）。
每一帧描述了一个代码中导致错误生成的调用点。
V8 引擎会试图显示每个函数的名称（变量名、函数名、或对象的方法名），但偶尔也可能找不到一个合适的名称。
如果 V8 引擎没法确定一个函数的名称，则只显示帧的位置信息。
否则，在位置信息的旁边会显示明确的函数名。

注意，帧只由 JavaScript 函数产生。
例如，同步地执行一个名为 `cheetahify` 的 C++ 插件，且插件自身调用一个 JavaScript 函数，代表 `cheetahify` 回调的栈帧不会出现在堆栈跟踪里：


```js
const cheetahify = require('./native-binding.node');

function makeFaster() {
  // cheetahify 同步地调用 speedy.
  cheetahify(function speedy() {
    throw new Error('oh no!');
  });
}

makeFaster();
// will throw:
//   /home/gbusey/file.js:6
//       throw new Error('oh no!');
//           ^
//   Error: oh no!
//       at speedy (/home/gbusey/file.js:6:11)
//       at makeFaster (/home/gbusey/file.js:5:3)
//       at Object.<anonymous> (/home/gbusey/file.js:10:1)
//       at Module._compile (module.js:456:26)
//       at Object.Module._extensions..js (module.js:474:10)
//       at Module.load (module.js:356:32)
//       at Function.Module._load (module.js:312:12)
//       at Function.Module.runMain (module.js:497:10)
//       at startup (node.js:119:16)
//       at node.js:906:3
```

位置信息会是其中之一：

* `native`，帧表示一个 V8 引擎内部的调用（比如，`[].forEach`）。
* `plain-filename.js:line:column`，帧表示一个 Node.js 内部的调用。
* `/absolute/path/to/file.js:line:column`，帧表示一个用户程序或其依赖的调用。

代表堆栈跟踪的字符串是在 `error.stack` 属性被访问时才生成的。

堆栈跟踪捕获的帧的数量是由 `Error.stackTraceLimit` 或当前事件循环中可用的帧数量的最小值界定的。

系统级的错误是由扩展的 `Error` 实例产生的，详见[系统错误]。

