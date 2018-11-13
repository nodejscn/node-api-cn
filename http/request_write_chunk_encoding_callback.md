<!-- YAML
added: v0.1.29
-->

* `chunk` {string | Buffer}
* `encoding` {string}
* `callback` {Function}
* 返回: {boolean}

发送请求主体的一个数据块。
通过多次调用该方法，完整的请求主体可被发送到服务器。
当创建请求时，建议使用 `['Transfer-Encoding', 'chunked']` 请求头。

`encoding` 参数是可选的，仅当 `chunk` 是字符串时才有效。
默认为 `'utf8'`。

`callback` 参数是可选的，当数据块被刷新且不为空时调用。

如果完整的数据被成功地刷新到内部缓冲，则返回 `true`。
如果失败或部分数据还在内存中等待队列，则返回 `false`。
当缓冲再次可用时触发 `'drain'` 事件。

当调用 `write` 函数传入空字符串或空 buffer 时，不会进行任何操作。

