
使用以下环境变量，可以自定义 Node.js REPL 的各种行为：

 - `NODE_REPL_HISTORY` - 当给定了一个有效的路径，则 REPL 的历史记录将被保存到指定的文件，而不是用户目录下的 `.node_repl_history` 文件。
  设为 `""` 将禁用 REPL 历史记录。
  值两头的空格键会被去掉。
 - `NODE_REPL_HISTORY_SIZE` - 默认为 `1000`。控制历史记录的最大行数。必须是正数。
 - `NODE_REPL_MODE` - 可以是 `sloppy`、`strict` 或 `magic`。
  Defaults to `sloppy`, which will allow non-strict mode code to be run. `magic` is
   **deprecated** and treated as an alias of `sloppy`.

