<!-- YAML
added: v0.11.2
-->

`writable.uncork()` 将输出在 [`stream.cork()`][] 方法被调用之后缓冲在内存中的所有数据。

如果使用 [`writable.cork()`] 和 `writable.uncork()` 来管理写入缓存，建议使用 `process.nextTick()` 来延迟调用 `writable.uncork()` 方法。通过这种方式，可以对单个 Node.js 事件循环中调用的所有 `writable.write()` 方法进行批处理。

```js
stream.cork();
stream.write('some ');
stream.write('data ');
process.nextTick(() => stream.uncork());
```

如果一个流多次调用了 [`writable.cork()`] 方法，那么也必须调用同样次数的 `writable.uncork()` 方法以输出缓冲区数据。

```js
stream.cork();
stream.write('some ');
stream.cork();
stream.write('data ');
process.nextTick(() => {
  stream.uncork();
  // 之前的数据只有在 uncork() 被二次调用后才会输出
  stream.uncork();
});
```

也可查看 [`writable.cork()`]。

