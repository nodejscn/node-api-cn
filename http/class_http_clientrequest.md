<!-- YAML
added: v0.1.17
-->

`http.ClientRequest` 实例由 [`http.request()`] 内部创建并返回。
表示一个正在进行中的请求，且请求头已进入队列。
请求头仍可使用 [`setHeader(name, value)`]、[`getHeader(name)`] 或 [`removeHeader(name)`] 进行修改。
最终的请求头会与第一个数据块一起发送或当调用 [`request.end()`] 时发送。

如果要获取响应，则需添加监听器到 `http.ClientRequest` 实例的 [`'response'`] 事件。
当接收到响应头时，会触发 [`'response'`] 事件。
[`'response'`] 事件有一个参数，该参数是 [`http.IncomingMessage`] 实例。

在 [`'response'`] 事件期间，可以添加监听器到 `http.IncomingMessage` 实例，比如监听 `'data'` 事件。

如果没有添加 [`'response'`] 事件句柄，则响应会被丢弃。
如果添加了句柄，则必须消费完响应对象的数据，可以调用 `response.read()`、或添加 `'data'` 事件句柄、或调用 `.resume()`。
当数据被消费完时会触发 `'end'` 事件。
在数据被读取完之前会消耗内存，可能会造成 `'process out of memory'` 错误。

Node.js 不会检查 `Content-Length` 与已传输的请求主体的长度是否相等。

`http.ClientRequest` 类继承自[流][Stream]。

