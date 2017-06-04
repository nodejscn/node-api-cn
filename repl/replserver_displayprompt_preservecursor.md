<!-- YAML
added: v0.1.91
-->

* `preserveCursor` {boolean}

`replServer.displayPrompt()` 方法会让 REPL 实例做好用户输入的准备，打印配置的 `prompt` 到 `output` 中新的一行，然后返回 `input` 等待新的输入。

当正在键入多行输入时，会打印省略号而不是提示符。

当 `preserveCursor` 为 `true` 时，游标位置不会被复位到 `0`。

`replServer.displayPrompt` 方法主要被使用 `replServer.defineCommand()` 方法注册的命令的 `action` 函数调用。

