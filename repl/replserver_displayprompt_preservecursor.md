<!-- YAML
added: v0.1.91
-->

* `preserveCursor` {Boolean}

`replServer.displayPrompt()` 方法会准备好 REPL 实例用于用户输入、打印配置的 `prompt` 到 `output` 中新的一行、恢复 `input` 来接收新的输入。

当正在键入多行输入时，会打印省略号而不是提示符。

当 `preserveCursor` 为 `true` 时，光标落点不会被重置为 `0`。

`replServer.displayPrompt` 方法主要被使用 `replServer.defineCommand()` 方法注册的命令的 `action` 函数调用。

