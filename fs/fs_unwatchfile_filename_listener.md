<!-- YAML
added: v0.1.31
-->

* `filename` {string|Buffer|URL}
* `listener` {Function} 可选的，之前使用 `fs.watchFile()` 绑定的监听器。

停止监视 `filename` 的变化。
如果指定了 `listener`，则仅移除此特定监听器，否则，将移除所有监听器，从而停止监视 `filename`。

对未被监视的文件名调用 `fs.unwatchFile()` 将是空操作，而不是错误。

使用 [`fs.watch()`] 比 `fs.watchFile()` 和 `fs.unwatchFile()` 更高效。
应尽可能使用 `fs.watch()` 代替 `fs.watchFile()` 和 `fs.unwatchFile()`。

