
对于高级的行编辑器，可以使用环境变量 `NODE_NO_READLINE=1` 来启动 Node.js。
这会以标准的终端配置来启动主 REPL 和调试 REPL，可以使用 `rlwrap`。

例如，可以在 `.bashrc` 文件中添加：

```text
alias node="env NODE_NO_READLINE=1 rlwrap node"
```

