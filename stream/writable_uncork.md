<!-- YAML
added: v0.11.2
-->

将调用 [`stream.cork()`][] 后缓冲的所有数据输出到目标。

当使用 [`writable.cork()`] 和 `writable.uncork()` 来管理流的写入缓冲时，建议使用 `process.nextTick()` 来延迟调用 `writable.uncork()`。
通过这种方式，可以对单个 Node.js 事件循环中调用的所有 `writable.write()` 进行批处理。

```js
stream.cork();
stream.write('一些 ');
stream.write('数据 ');
process.nextTick(() => stream.uncork());
```

如果一个流上多次调用 [`writable.cork()`]，则必须调用同样次数的 `writable.uncork()` 才能输出缓冲的数据。

```js
stream.cork();
stream.write('一些 ');
stream.cork();
stream.write('数据 ');
process.nextTick(() => {
  stream.uncork();
  // 数据不会被输出，直到第二次调用 uncork()。
  stream.uncork();
});
```

