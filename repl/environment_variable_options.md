
使用以下环境变量，可以自定义 Node.js REPL 的各种行为：

 - `NODE_REPL_HISTORY` - 当给定了一个有效的路径，则 REPL 的历史记录将被保存到指定的文件，而不是用户目录下的 `.node_repl_history` 文件。
  设为 `''`（空字符串）将会禁用持久的 REPL 历史记录。
  值两头的空格键会被去掉。
  在 Windows 平台上，具有空值的环境变量是无效的，因此将此变量设置为一个或多个空格可以禁用持久的 REPL 历史记录。
 - `NODE_REPL_HISTORY_SIZE` - 控制历史记录的最大行数。必须是正数。**默认值:** `1000`。
 - `NODE_REPL_MODE` - 可以是 `'sloppy'` 或 `'strict'`。
  **默认值:** `'sloppy'`，允许代码在非严格模式下运行。

