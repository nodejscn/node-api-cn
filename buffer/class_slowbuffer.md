<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.allocUnsafeSlow()`] 代替。

Returns an un-pooled `Buffer`.

In order to avoid the garbage collection overhead of creating many individually
allocated `Buffer` instances, by default allocations under 4KB are sliced from a
single larger allocated object. This approach improves both performance and memory
usage since v8 does not need to track and cleanup as many `Persistent` objects.

In the case where a developer may need to retain a small chunk of memory from a
pool for an indeterminate amount of time, it may be appropriate to create an
un-pooled `Buffer` instance using `SlowBuffer` then copy out the relevant bits.

Example:

```js
// Need to keep around a few small chunks of memory
const store = [];

socket.on('readable', () => {
  const data = socket.read();

  // Allocate for retained data
  const sb = SlowBuffer(10);

  // Copy the data into the new allocation
  data.copy(sb, 0, 0, 10);

  store.push(sb);
});
```

Use of `SlowBuffer` should be used only as a last resort *after* a developer
has observed undue memory retention in their applications.

