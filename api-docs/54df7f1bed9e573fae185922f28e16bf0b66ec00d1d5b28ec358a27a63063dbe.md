
当 `writable._write()` 和 `writable._writev()` 在执行期间发生的错误时，建议调用回调函数并传入错误对象作为第一个参数。
这样 `Writable` 就会触发 `'error'` 事件。
从 `writable._write()` 中抛出错误可能会导致无法预期的结果。
使用回调可以确保对错误进行一致且可预测的处理。

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('无效的数据块'));
    } else {
      callback();
    }
  }
});
```

