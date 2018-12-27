<!-- YAML
added: v5.12.0
-->

* `size` {integer} 新建的 `Buffer` 的长度。

创建一个大小为 `size` 字节的 `Buffer`。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`ERR_INVALID_OPT_VALUE`]。
如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

以这种方式创建的 `Buffer` 的内存是未初始化的。
`Buffer` 的内容是未知的，可能包含敏感数据。
使用 [`buf.fill(0)`][`buf.fill()`] 可以初始化 `Buffer`。

当使用 [`Buffer.allocUnsafe()`] 创建 `Buffer` 时，如果要分配的内存小于 4KB，则会从一个预分配的 `Buffer` 切割出来。
这可以避免垃圾回收机制因创建太多独立的 `Buffer` 而过度使用。

当需要在内存池保留一小块内存时，可以使用 `Buffer.allocUnsafeSlow()` 创建一个非内存池的 `Buffer` 并拷贝出来。

```js
// 保留一小块内存。
const store = [];

socket.on('readable', () => {
  const data = socket.read();

  // 分配内存。
  const sb = Buffer.allocUnsafeSlow(10);

  // 拷贝数据到内存。
  data.copy(sb, 0, 0, 10);

  store.push(sb);
});
```

