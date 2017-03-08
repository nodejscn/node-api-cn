
For advanced line-editors, start Node.js with the environmental variable
`NODE_NO_READLINE=1`. This will start the main and debugger REPL in canonical
terminal settings which will allow you to use with `rlwrap`.
高级的命令行编辑者，可以使用环境变量`NODE_NO_READLINE=1`来启动Node.js。这将使用
官方终端设置启动主REPL和调试REPL，这可以允许你使用`rlwrap`工具。

For example, you could add this to your bashrc file:
举例，你可以在你的bashrc文件中添加：
```text
alias node="env NODE_NO_READLINE=1 rlwrap node"
```

