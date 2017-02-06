<!-- YAML
added: v0.1.29
-->

* `chunk` {String | Buffer}
* `encoding` {String}
* `callback` {Function}
* 返回: {Boolean}

如果该方法被调用且 [`response.writeHead()`] 还未被调用，则它会切换到隐式消息头模式并刷新隐式消息头。

它会发送一块响应主体。
该方法可被多次调用，以便提供主体连续的部分。

`chunk` 可以是一个字符串或一个 buffer。
如果 `chunk` 是一个字符串，则第二个参数指定如何将它编码成一个字节流。
`encoding` 默认为 `'utf8'`。
当数据块被刷新时，`callback` 会被调用。

**注意**：这是原始的 HTTP 主体，且与可能使用的更高级别的多部分主体编码无关。

[`response.write()`] 首次被调用时，它会发送缓冲的头信息和第一块主体到客户端。
[`response.write()`] 第二次被调用时，Node.js 会假定你要流化数据，并将它们分别发送。
响应会被缓冲到主体的第一个数据块。

如果整个数据被成功刷新到内核缓冲区，则返回 `true`。
如果全部或部分数据在用户内存中排队，则返回 `false`。
当缓冲区再次空闲时，则触发 `'drain'` 事件。

