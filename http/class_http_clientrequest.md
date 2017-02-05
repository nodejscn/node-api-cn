<!-- YAML
added: v0.1.17
-->

该对象在内部被创建，并从 [`http.request()`] 返回。
它表示着一个**正在处理**的请求，其请求头已进入队列。
请求头仍可使用 `setHeader(name, value)`、`getHeader(name)` 和 `removeHeader(name)` API 进行修改。
实际的请求头会与第一个数据块或关闭连接时一起被发送。

要获取响应，需添加一个 [`'response'`] 监听器到请求对象上。
当响应头被接收时，请求对象会触发 [`'response'`]。
[`'response'`] 事件被执行时带有一个参数，该参数是一个 [`http.IncomingMessage`] 实例。

在 [`'response'`] 事件期间，可以添加监听器到响应对象；比如监听 `'data'` 事件。

如果没有添加 [`'response'`] 句柄，则响应会被完全丢弃。
当然，如果添加了 [`'response'`] 事件句柄，则**必须**消耗响应对象的数据（当有 `'readable'` 事件时调用 `response.read()`、或添加一个 `'data'` 句柄、或调用 `.resume()` 方法）。
`'end'` 事件不会被触发，直到数据被消耗完。
同样，在数据读完之前，它会消耗内存，可能会造成 'process out of memory' 错误。

注意：Node.js 不会检查 Content-Length 和已发送的主体的长度是否相等。

请求实现了[可写流]接口。
这是一个包含以下事件的 [`EventEmitter`]：

