<!-- YAML
added: v0.1.31
-->

* `filename` {string|Buffer|URL}
* `listener` {Function} 已使用 `fs.watchFile()` 绑定的监听器。

停止监视 `filename` 文件的变化。
如果指定了 `listener`，则只移除特定的监听器，否则移除全部监听器，且停止监视 `filename`。

调用 `fs.unwatchFile()` 且带上一个未被监视的文件名，将会是一个空操作，而不是一个错误。

[`fs.watch()`] 比 `fs.watchFile()` 和 `fs.unwatchFile()` 更高效。
建议使用 `fs.watch()` 而不是 `fs.watchFile()` 和 `fs.unwatchFile()`。

