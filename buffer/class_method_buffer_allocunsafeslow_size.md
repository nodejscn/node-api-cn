<!-- YAML
added: v5.10.0
-->

* `size` {integer} 新建的 `Buffer` 期望的长度

分配一个大小为 `size` 字节的新建的 `Buffer` 。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`RangeError`] 错误。
如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

以这种方式创建的 `Buffer` 实例的底层内存是**未初始化**的。
新创建的 `Buffer` 的内容是未知的，且**可能包含敏感数据**。
可以使用 [`buf.fill(0)`] 初始化 `Buffer` 实例为0。

当使用 [`Buffer.allocUnsafe()`] 分配新建的 `Buffer` 时，当分配的内存小于 4KB 时，默认会从一个单一的预分配的 `Buffer` 切割出来。
这使得应用程序可以避免垃圾回收机制因创建太多独立分配的 `Buffer` 实例而过度使用。
这个方法通过像大多数持久对象一样消除追踪与清理的需求，改善了性能与内存使用。

当然，在开发者可能需要在不确定的时间段从内存池保留一小块内存的情况下，使用 `Buffer.allocUnsafeSlow()` 创建一个非池的 `Buffer` 实例然后拷贝出相关的位元是合适的做法。

例子：

```js
// 需要保留一小块内存块
const store = [];

socket.on('readable', () => {
  const data = socket.read();

  // 为保留的数据分配内存
  const sb = Buffer.allocUnsafeSlow(10);

  // 拷贝数据进新分配的内存
  data.copy(sb, 0, 0, 10);

  store.push(sb);
});
```

`Buffer.allocUnsafeSlow()` 应当仅仅作为开发者已经在他们的应用程序中观察到过度的内存保留之后的终极手段使用。

如果 `size` 不是一个数值，则抛出 `TypeError` 错误。

