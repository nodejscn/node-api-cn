<!-- YAML
added: v0.3.0
-->

* `keyword` {String} 命令关键字（*除了*先导的`.`字符）。
* `cmd` {Object|Function} 当命令被执行完后调用的函数。

`replServer.defineCommand()`函数是用来增加新的`.`前缀的命令到REPL实例中。这些命
令通过输入一个`.`加`keyword`的指令来调用。`cmd`既是一个函数也是一个对象，具备以下属性：

* `help` {String} 输入`.help`后显示帮助文字（可选）。
* `action` {Function} 命令要执行的函数，可选接受一个string参数。

接下来的例子展示两个新的命令，增加到REPL实例中：

```js
const repl = require('repl');

var replServer = repl.start({prompt: '> '});
replServer.defineCommand('sayhello', {
  help: 'Say hello',
  action: function(name) {
    this.lineParser.reset();
    this.bufferedCommand = '';
    console.log(`Hello, ${name}!`);
    this.displayPrompt();
  }
});
replServer.defineCommand('saybye', function() {
  console.log('Goodbye!');
  this.close();
});
```

接下来，可以在REPL实例中使用新的命令：

```txt
> .sayhello Node.js User
Hello, Node.js User!
> .saybye
Goodbye!
```

