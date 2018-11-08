<!-- YAML
added: v0.5.8
-->

调用 [`fs.watch()`] 会返回一个 `fs.FSWatcher` 对象。

所有 `fs.FSWatcher` 对象都是 [`EventEmitter`] 的实例，每当监视的文件被修改时都会触发 `'change'` 事件。

