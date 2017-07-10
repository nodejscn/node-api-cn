<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.allocUnsafeSlow()`] 代替。

返回一个不放入分配池的 `Buffer`。

为了避免垃圾回收机制因创建太多独立分配的 Buffer 实例而过度使用，默认小于 4KB 的内存会从一个单一的大内存中切割出来。这种方式可以有效提高性能和内存利用率，避免 V8 频繁追踪和清理过多的 Persistent 对象。

开发者可能需要在不确定的时间段从内存池保留一小块内存的情况下，针对这种情况，就可以使用 `SlowBuffer` 类创建不放入分配池 `Buffer` 实例，然后通过内存拷贝获取目标数据。

例子:

```js
// 需要保存的一小块内存
const store = [];

socket.on('readable', () => {
  const data = socket.read();

  // 为保留的数据分配内存
  const sb = SlowBuffer(10);

  // 将数据复制到新的分配的内存中
  data.copy(sb, 0, 0, 10);

  store.push(sb);
});
```

`SlowBuffer` 应当仅仅作为开发者已经在他们的应用程序中观察到过度的内存保留之后的终极手段使用。
