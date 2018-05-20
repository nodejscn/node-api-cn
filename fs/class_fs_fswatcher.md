<!-- YAML
added: v0.5.8
-->

成功调用 [`fs.watch()`] 方法会返回一个新的 `fs.FSWatcher` 对象。

所有 `fs.FSWatcher` 对象都是 [`EventEmitter`] 的，每当监视的文件被修改时会触发 `'change'` 事件。

