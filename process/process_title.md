<!-- YAML
added: v0.1.104
-->

* {string}

`process.title` 属性返回当前进程标题（即返回 `ps` 的当前值）。 
为 `process.title` 分配新值会修改 `ps` 的当前值。

当分配新值时，不同的平台会对标题施加不同的最大长度限制。 
通常这种限制是相当有限的。 
例如，在 Linux 和 macOS 上，`process.title` 仅限于二进制名称的大小加上命令行参数的长度，因为设置 `process.title` 会覆盖进程的 `argv` 内存。
Node.js 的 v0.8, 通过覆盖 `environ` 允许内存较长的过程标题字符串，但是这在一些（相当模糊的）可能是不安全的并且令人困惑情况下。
