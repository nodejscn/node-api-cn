<!-- YAML
added: v0.1.17
-->

该对象在 [`http.request()`] 内部被创建并返回。
它表示着一个正在处理的请求，其请求头已进入队列。
请求头仍可使用 `setHeader(name, value)`、`getHeader(name)` 和 `removeHeader(name)` API 进行修改。
实际的请求头会与第一个数据块一起发送或当关闭连接时发送。

要获取响应，需为 [`'response'`] 事件添加一个监听器到请求对象上。
当响应头被接收到时，[`'response'`] 事件会从请求对象上被触发 。
[`'response'`] 事件被执行时带有一个参数，该参数是一个 [`http.IncomingMessage`] 实例。

在 [`'response'`] 事件期间，可以添加监听器到响应对象上，比如监听 `'data'` 事件。

如果没有添加 [`'response'`] 事件处理函数，则响应会被整个丢弃。
如果添加了 [`'response'`] 事件处理函数，则必须消耗完响应对象的数据，可通过调用 `response.read()`、或添加一个 `'data'` 事件处理函数、或调用 `.resume()` 方法。
数据被消耗完时会触发 `'end'` 事件。
在数据被读取完之前会消耗内存，可能会造成 `'process out of memory'` 错误。

注意：Node.js 不会检查 `Content-Length` 与已传输的请求主体的长度是否相等。

该请求实现了 [可写流] 接口。
它是一个包含以下事件的 [`EventEmitter`]：

