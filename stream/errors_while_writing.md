
在 [`writable._write()`]、[`writable._writev()`] 和 [`writable._final()`] 方法的处理期间发生的错误必须通过调用回调并将错误作为第一个参数传入来冒泡。 
从这些方法中抛出 `Error` 或手动触发 `'error'` 事件会导致未定义的行为。

如果 `Readable` 流通过管道传送到 `Writable` 流时 `Writable` 触发了错误，则 `Readable` 流将会被取消管道。

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('数据块是无效的'));
    } else {
      callback();
    }
  }
});
```

