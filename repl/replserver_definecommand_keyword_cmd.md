<!-- YAML
added: v0.3.0
-->

* `keyword` {String} 命令关键字（开头不带 `.` 字符）。
* `cmd` {Object|Function} 当命令被执行时调用的函数。

`replServer.defineCommand()` 方法用于添加新的前缀为 `.` 的命令到 REPL 实例。
这些命令通过输入 `.` 并带上 `keyword` 来调用。
`cmd` 是一个函数或一个有以下属性的对象：

* `help` {String} 当键入 `.help` 时显示的帮助说明（可选）。
* `action` {Function} 要执行的函数，可接受一个字符串参数。

例子，添加两个新命令到 REPL 实例：

```js
const repl = require('repl');

var replServer = repl.start({prompt: '> '});
replServer.defineCommand('sayhello', {
  help: '打招呼',
  action: function(name) {
    this.lineParser.reset();
    this.bufferedCommand = '';
    console.log(`你好，${name}！`);
    this.displayPrompt();
  }
});
replServer.defineCommand('saybye', function() {
  console.log('再见！');
  this.close();
});
```

在 REPL 实例中使用新的命令：

```txt
> .sayhello Node.js中文网
你好，Node.js中文网！
> .saybye
再见！
```

