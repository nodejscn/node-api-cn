<!-- YAML
added: v0.5.8
-->

* 继承自 {EventEmitter}

成功调用 [`fs.watch()`] 方法会返回新建的 `fs.FSWatcher` 对象。

每当指定监视的文件被修改时，所有的 `fs.FSWatcher` 对象都会触发 `'change'` 事件。

