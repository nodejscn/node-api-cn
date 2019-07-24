<!-- YAML
added: v11.10.0
-->

* `historyPath` {string} 历史文件的路径。
* `callback` {Function} 当历史记录写入已准备好或出错时调用。
  * `err` {Error}
  * `repl` {repl.REPLServer}

初始化 REPL 实例的历史记录日志文件。 
当执行 Node.js 二进制文件并使用命令行 REPL 时，默认情况下会初始化历史记录文件。 
但是，以编程方式创建 REPL 时不是这种情况。 
当以编程方式使用 REPL 实例时，使用此方法初始化历史记录日志文件。

