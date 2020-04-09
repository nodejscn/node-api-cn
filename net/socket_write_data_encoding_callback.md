<!-- YAML
added: v0.1.90
-->

* `data` {string|Buffer|Uint8Array}
* `encoding` {string} 仅在数据为 `string` 时使用。**默认值:** `utf8`。
* `callback` {Function}
* 返回: {boolean}

在 socket 上发送数据。第二个参数制定了字符串的编码。
默认是 UTF8 编码。

如果全部数据都成功刷新到内核的缓冲则返回 `true`。如果全部或部分数据在用户内中排队，则返回 `false`。当缓冲再次空闲的时候将触发 [`'drain'`][] 事件。

当数据最终都被写出之后，可选的 `callback` 参数将会被执行（可能不会立即执行）。

详见 `Writable` 流的 [`write()`][stream_writable_write] 方法。


