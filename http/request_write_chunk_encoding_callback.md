<!-- YAML
added: v0.1.29
-->

* `chunk` {string|Buffer}
* `encoding` {string}
* `callback` {Function}
* 返回: {boolean}

发送一个请求主体的数据块。 
通过多次调用此方法，可以将请求主体发送到服务器，在这种情况下，建议在创建请求时使用 `['Transfer-Encoding', 'chunked']` 请求头行。

`encoding` 参数是可选的，仅当 `chunk` 是字符串时才适用。
默认为 `'utf8'`。

`callback` 参数是可选的，当刷新此数据块时调用，但仅当数据块非空时才会调用。

如果将整个数据成功刷新到内核缓冲区，则返回 `true`。 
如果全部或部分数据在用户内存中排队，则返回 `false`。 
当缓冲区再次空闲时，则触发 `'drain'` 事件。

当使用空字符串或 buffer 调用 `write` 函数时，则什么也不做且等待更多输入。

