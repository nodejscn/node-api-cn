
By default, all instances of `repl.REPLServer` use an evaluation function that
evaluates JavaScript expressions and provides access to Node.js' built-in
modules. This default behavior can be overridden by passing in an alternative
evaluation function when the `repl.REPLServer` instance is created.

默认情况下，所有`repl.REPLServer`的实例使用一个解释函数，它可以解释JavaScript表达式
并提供连接内置的Node.js模块。`repl.REPLServer`实例创建的时候可以替换其解释函数，这样
可以覆盖其默认的功能。
