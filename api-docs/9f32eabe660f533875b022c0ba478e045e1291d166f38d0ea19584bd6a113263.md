<!-- YAML
added: v9.0.0
-->

`replServer.clearBufferedCommand()` 方法清除已缓冲但尚未执行的任何命令。 
此方法主要用于在使用 `replServer.defineCommand()` 方法注册的命令的 action 函数内调用。


