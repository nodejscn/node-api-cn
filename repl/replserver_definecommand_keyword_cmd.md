<!-- YAML
added: v0.3.0
-->

* `keyword` {string} 命令关键字（开头不带 `.` 字符）。
* `cmd` {Object|Function} 当命令被执行时调用的函数。

`replServer.defineCommand()` 方法用于添加新的前缀为 `.` 的命令到 REPL 实例。
这些命令通过输入一个 `.` 加 `keyword` 来调用。
`cmd` 可以是一个函数或一个具有以下属性的对象：

* `help` {string} 当键入 `.help` 时显示的帮助说明（可选）。
* `action` {Function} 要执行的函数，可接受一个字符串参数。

例子，添加两个新命令到 REPL 实例：

```js
const repl = require('repl');

const replServer = repl.start({ prompt: '> ' });
replServer.defineCommand('sayhello', {
  help: '打招呼',
  action(name) {
    this.lineParser.reset();
    this.bufferedCommand = '';
    console.log(`你好，${name}！`);
    this.displayPrompt();
  }
});
replServer.defineCommand('saybye', function saybye() {
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

