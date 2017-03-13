<!-- YAML
added: v2.0.0
deprecated: v3.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [NODE_REPL_HISTORY] 代替。

Node.js/io.js v2.x 之前，REPL 的历史记录使用 `NODE_REPL_HISTORY_FILE` 变量来控制，且历史记录以 JSON 格式保存。
该变量已被废弃，旧的 JSON 格式的 REPL 历史记录文件会被自动转换为一种精简的纯文本格式。
这个新的文件会被保存到用户目录下或由 `NODE_REPL_HISTORY` 变量定义的目录下，详见[环境变量选项]。

