<!-- YAML
added: v5.12.0
-->

* `size` {integer} 新建的 `Buffer` 的长度。

创建一个大小为 `size` 字节的新 `Buffer`。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`ERR_INVALID_OPT_VALUE`]。
如果 `size` 为 0，则创建一个长度为零的 `Buffer`。

以这种方式创建的 `Buffer` 实例的底层内存是未初始化的。
`Buffer` 的内容是未知的，可能包含敏感数据。
使用 [`buf.fill(0)`][`buf.fill()`] 可以以零初始化 `Buffer` 实例。

当使用 [`Buffer.allocUnsafe()`] 创建新的 `Buffer` 实例时，如果要分配的内存小于 4KB，则会从一个预分配的 `Buffer` 切割出来。
这可以避免垃圾回收机制因创建太多独立的 `Buffer` 而过度使用。
这种方式通过消除跟踪和清理的需要来改进性能和内存使用。

当开发人员需要在内存池中保留一小块内存时，可以使用 `Buffer.allocUnsafeSlow()` 创建一个非内存池的 `Buffer` 实例并拷贝相关的比特位出来。

```js
// 需要保留一小块内存。
const store = [];

socket.on('readable', () => {
  let data;
  while (null !== (data = readable.read())) {
    // 为剩下的数据分配内存。
    const sb = Buffer.allocUnsafeSlow(10);

    // 拷贝数据到新分配的内存。
    data.copy(sb, 0, 0, 10);

    store.push(sb);
  }
});
```

`Buffer.allocUnsafeSlow()` 应该只用作开发人员已经在其应用程序中观察到过度的内存之后的最后手段。

如果 `size` 不是一个数字，则抛出 `TypeError`。
