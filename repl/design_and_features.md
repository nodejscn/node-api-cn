
`repl` 模块导出了 `repl.REPLServer` 类。
当 `repl.REPLServer` 的实例运行时，它接收用户输入的每一行，使用用户定义的解释函数解释这些表达式，最终输出结果。
输入可以是 `stdin`、输出可以是`stdout`，或者也可以连接到其他任何 Node.js [流]。

`repl.REPLServer` 的实例支持输入的自动完成、精简 Emacs 风格的命令行编辑、多行输入、ANSI 风格输出、当前 REPL 会话状态的保存和恢复、错误恢复以及用户自定义的解释函数。

