<!-- YAML
added: v2.0.0
deprecated: v3.0.0
-->

> Stability: 0 - Deprecated: Use `NODE_REPL_HISTORY` instead.
> 稳定性： 0 - 不建议：使用`NODE_REPL_HISTORY`替代

Previously in Node.js/io.js v2.x, REPL history was controlled by using a
`NODE_REPL_HISTORY_FILE` environment variable, and the history was saved in JSON
format. This variable has now been deprecated, and the old JSON REPL history
file will be automatically converted to a simplified plain text format. This new
file will be saved to either the user's home directory, or a directory defined
by the `NODE_REPL_HISTORY` variable, as documented in the
[Environment Variable Options](#repl_environment_variable_options).
之前在Node.js/io.js v2.x，REPL的历史记录是用`NODE_REPL_HISTORY_FILE`变量来控制，历
史记录使用JSON格式保存。该变量已经不建议使用，旧的JSON格式REPL历史文件会被自动转化为
另一种简化的纯文本格式。该文件既可以保存在用户目录下或由`NODE_REPL_HISTORY`变量定义的
目录下，参见
[Environment Variable Options](#repl_environment_variable_options)
