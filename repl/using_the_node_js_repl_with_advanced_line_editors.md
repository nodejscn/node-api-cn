
对于高级的命令行编辑器，可以使用环境变量 `NODE_NO_READLINE=1` 来启动 Node.js。
这将使用官方终端设置启动主 REPL 和调试 REPL，这可以允许你使用 `rlwrap`工具。

举例，你可以在你的 bashrc 文件中添加：

```text
alias node="env NODE_NO_READLINE=1 rlwrap node"
```

