<!-- YAML
added: v2.0.0
deprecated: v3.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [NODE_REPL_HISTORY] 代替。

之前在 Node.js/io.js v2.x，REPL 的历史记录是用 `NODE_REPL_HISTORY_FILE` 变量来控制，历史记录使用 JSON 格式保存。
该变量已经不建议使用，旧的 JSON 格式 REPL 历史文件会被自动转化为另一种简化的纯文本格式。
该文件既可以保存在用户目录下或由 `NODE_REPL_HISTORY` 变量定义的目录下，参见[环境变量选项]。

