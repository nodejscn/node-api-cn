<!-- YAML
added: v0.11.14
-->

> 稳定性: 0 - 失效。一个替代方案正在开发中。

* `code` {string} 要被编译和执行的JavaScript代码

`vm.runInDebugContext()`会在V8的调试上下文中编译并执行`code`。此方法主要在需要获取V8`Debug`对象的时候使用。

```js
const vm = require('vm')
const Debug = vm.runInDebugContext('Debug');
console.log(Debug.findScript(process.emit).name);  // 'events.js'
console.log(Debug.findScript(process.exit).name);  // 'internal/process.js'
```

*注意*: 调试上下文和对象从本质而言是从属于V8调试器的，故有可能会在没有事先警告的情况下被改变（甚至被移除）

`Debug`对象另外还可以通过特定于V8的`--expose_debug_as`[命令行选项][command line option]获得。

