
使用以下环境变量，可以定制 Node.js 的 REPL 的多种行为：

 - `NODE_REPL_HISTORY` - 一旦设置一个有效路径，REPL 历史记录将被保存到指定的文件中而不是用户目录下的 `.node_repl_history` 文件。
  把该变量设置为 `""` 将禁用 REPL 历史记录。
  空格键会被自动从值中裁剪掉。
 - `NODE_REPL_HISTORY_SIZE` - 默认值 `1000`。控制历史记录的最大行数。必须是正数。
 - `NODE_REPL_MODE` - 可以是 `sloppy`, `strict` 或 `magic`。
  默认是 `magic`，`strict` 模式中会自动运行 "strict mode only" 状态。

