<!-- YAML
added: v0.1.91
-->

* `preserveCursor` {Boolean}

`replServer.displayPrompt()`方法让REPL实例做好用户输入的准备，在`输出`界面中新的一行打印
设置好的`提示符`，然后返回`输入`等待新的输入。
进入多行输入模式后，显示省略符号而不是`提示符`。

当`preserveCursor`为`true`,游标位置会被复位到`0`。

`replServer.displayPrompt`方法主要是用在`replServer.defineCommand()`函数注册的命令中
的`action`函数中被调用。
