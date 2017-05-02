<!-- YAML
added: v0.1.29
-->

* `chunk` {String | Buffer}
* `encoding` {String}
* `callback` {Function}

发送请求主体的一个数据块。
通过多次调用该方法，用户可以以流的形式将请求主体发送到服务器，在这种情况下，当创建请求时，建议使用 `['Transfer-Encoding', 'chunked']` 请求头。

`encoding` 参数是可选的，仅当 `chunk` 是一个字符串时才有效。默认为 `'utf8'`。

`callback` 参数是可选的，当数据块被刷新时调用。

返回 `request`。

