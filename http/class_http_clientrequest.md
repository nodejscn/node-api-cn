<!-- YAML
added: v0.1.17
-->

* 继承自: {Stream}

此对象由 [`http.request()`] 内部创建并返回。
它表示正在进行中的请求（请求头已进入队列）。
请求头仍然可以使用 [`setHeader(name, value)`]、[`getHeader(name)`] 或 [`removeHeader(name)`] API 进行改变。
实际的请求头会与第一个数据块一起发送，或者当调用 [`request.end()`] 时发送。

若要获取响应，则添加 [`'response'`] 事件监听器到请求对象。
当响应头已被接收时，则会从请求对象中触发 [`'response'`] 事件。 
[`'response'`] 事件被执行时有一个参数，该参数是 [`http.IncomingMessage`] 的实例。

在 [`'response'`] 事件期间，可以添加监听器到响应对象，比如监听 `'data'` 事件。

如果没有添加 [`'response'`] 事件处理函数，则响应会被完全地丢弃。
但是，如果添加了 [`'response'`] 事件处理函数，则响应对象中的数据必须被消费（每当有 `'readable'` 事件时调用 `response.read()`、或添加 `'data'` 事件处理函数、或调用 `.resume()` 方法）。
在数据被消费完之前，不会触发 `'end'` 事件。
此外，在读取数据之前，它会占用内存，这可能最终会导致进程内存不足的错误。

与 `request` 对象不同，如果响应过早地关闭，则 `response` 对象不会触发 `'error'` 事件而是触发 `'aborted'` 事件。

Node.js 不会检查 Content-Length 与已传输的请求体的长度是否相等。


