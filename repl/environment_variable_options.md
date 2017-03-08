
Various behaviors of the Node.js REPL can be customized using the following
environment variables:
使用以下环境变量，可以定制Node.js的REPL的多种行为：

 - `NODE_REPL_HISTORY` - When a valid path is given, persistent REPL history
   will be saved to the specified file rather than `.node_repl_history` in the
   user's home directory. Setting this value to `""` will disable persistent
   REPL history. Whitespace will be trimmed from the value.
 - `NODE_REPL_HISTORY` - 一旦设置一个有效路径，REPL历史记录将被保存到指定的文件中而不是用户目录下的`.node_repl_history`文件。
把该变量设置为`“”`将禁用REPL历史记录。空格键会被自动从值中裁剪掉。

 - `NODE_REPL_HISTORY_SIZE` - Defaults to `1000`. Controls how many lines of
   history will be persisted if history is available. Must be a positive number.
 - `NODE_REPL_HISTORY_SIZE` - 默认值`1000`。控制历史记录的最大行数。必须是正数。

 - `NODE_REPL_MODE` - May be any of `sloppy`, `strict`, or `magic`. Defaults
   to `magic`, which will automatically run "strict mode only" statements in
   strict mode.
 - `NODE_REPL_MODE` - 可以是`sloppy`, `strict`或`magic`。默认是`magic`，`strict`模式中会自动运行"strict mode only"状态。

