<!-- YAML
added: v0.1.104
-->
* `message` {any}
* `...args` {any}

打印字符串 `'Trace: '` 到 `stderr`，然后将 [`util.format()`] 格式化的消息和堆栈跟踪打印到代码中的当前位置。

```js
console.trace('展示');
// 打印: (堆栈跟踪将根据调用跟踪的位置而有所不同)
//  Trace: 展示
//    at repl:2:9
//    at REPLServer.defaultEval (repl.js:248:27)
//    at bound (domain.js:287:14)
//    at REPLServer.runBound [as eval] (domain.js:300:12)
//    at REPLServer.<anonymous> (repl.js:412:12)
//    at emitOne (events.js:82:20)
//    at REPLServer.emit (events.js:169:7)
//    at REPLServer.Interface._onLine (readline.js:210:10)
//    at REPLServer.Interface._line (readline.js:549:8)
//    at REPLServer.Interface._ttyWrite (readline.js:826:14)
```

