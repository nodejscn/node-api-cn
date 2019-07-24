<!-- YAML
added: v0.1.17
-->

此对象由 [`http.request()`] 内部创建并返回。
它表示正在进行的请求，且其请求头已进入队列。
请求头仍然可以使用 [`setHeader(name, value)`]、[`getHeader(name)`] 或 [`removeHeader(name)`] 改变。
实际的请求头将与第一个数据块一起发送，或者当调用 [`request.end()`] 时发送。

要获得响应，则为请求对象添加 [`'response'`] 事件监听器。
当接收到响应头时，将、则会从请求对象触发 [`'response'`] 事件。 
[`'response'`] 事件执行时有一个参数，该参数是 [`http.IncomingMessage`] 的实例。

在 [`'response'`] 事件期间，可以添加监听器到响应对象，比如监听 `'data'` 事件。

如果没有添加 [`'response'`] 事件处理函数，则响应将被完全丢弃。
如果添加了 [`'response'`] 事件处理函数，则必须消费完响应对象中的数据，每当有 `'readable'` 事件时调用 `response.read()`、或添加 `'data'` 事件处理函数、或通过调用 `.resume()` 方法。
在消费完数据之前，不会触发 `'end'` 事件。
此外，在读取数据之前，它将占用内存，最终可能导致进程内存不足的错误。

Node.js 不检查 Content-Length 和已传输的主体的长度是否相等。

请求继承自[流][Stream]，且额外实现以下内容：

