<!-- YAML
added: v0.1.29
-->

* `chunk` {string | Buffer}
* `encoding` {string}
* `callback` {Function}
* 返回: {boolean}

如果该方法被调用且 [`response.writeHead()`] 没有被调用，则它会切换到隐式响应头模式并刷新隐式响应头。

该方法会发送一块响应主体。
它可被多次调用，以便提供连续的响应主体片段。

Note that in the `http` module, the response body is omitted when the
request is a HEAD request. Similarly, the `204` and `304` responses
_must not_ include a message body.

`chunk` 可以是一个字符串或一个 buffer。
如果 `chunk` 是一个字符串，则第二个参数指定如何将它编码成一个字节流。
`encoding` 默认为 `'utf8'`。
当数据块被刷新时，`callback` 会被调用。

注意：这是原始的 HTTP 主体，且与可能被使用的高级主体编码无关。

[`response.write()`] 首次被调用时，会发送缓冲的响应头信息和响应主体的第一块数据到客户端。
[`response.write()`] 第二次被调用时，Node.js 会以流的形式处理数据，并将它们分别发送。
也就是说，响应会被缓冲到响应主体的第一个数据块。

如果全部数据被成功刷新到内核缓冲区，则返回 `true`。
如果全部或部分数据还在内存中排队，则返回 `false`。
当缓冲区再次空闲时，则触发 `'drain'` 事件。

