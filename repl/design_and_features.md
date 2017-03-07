
The `repl` module exports the `repl.REPLServer` class. While running, instances
of `repl.REPLServer` will accept individual lines of user input, evaluate those
according to a user-defined evaluation function, then output the result. Input
and output may be from `stdin` and `stdout`, respectively, or may be connected
to any Node.js [stream][].
`repl`模块用来导出`repl.REPLServer`类。当 `repl.REPLServer`的实例运行时，它接收
用户输入的每一行，使用用户定义的解释函数解释这些表达式，最终输出结果。输入可以是
`stdin`、输出可以是`stdout`，或者也可以连接到其他任何Node.js [流][].


Instances of `repl.REPLServer` support automatic completion of inputs,
simplistic Emacs-style line editing, multi-line inputs, ANSI-styled output,
saving and restoring current REPL session state, error recovery, and
customizable evaluation functions.
`repl.REPLServer`的实例支持输入的自动完成。精简Emacs风格的命令行编辑，多行输入，
ANSI风格输出，当前REPL会话状态的保存和回复，错误恢复以及用户自定义的解释函数。
