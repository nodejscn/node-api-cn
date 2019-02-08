<!-- YAML
added: v0.5.8
-->

成功调用 [`fs.watch()`] 方法将返回一个新的 `fs.FSWatcher` 对象。

所有 `fs.FSWatcher` 对象都是 [`EventEmitter`] 的实例，每当修改指定监视的文件，就会触发 `'change'` 事件。

