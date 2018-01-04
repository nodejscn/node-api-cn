
建议在处理`writable._write()`和`writable._writev()`方法期间发生的错误时传给回调函数的第一个参数来处理。这将导致Writable触发`error`事件。从`writable._write()`中抛出一个错误可能会导致意外和不一致的行为，具体取决于如何使用流。使用回调可确保对错误进行一致且可预测的处理。

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('chunk is invalid'));
    } else {
      callback();
    }
  }
});
```

