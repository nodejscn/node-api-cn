<!-- YAML
added: v0.5.8
-->
- `size` {number}
- `callback` {Function}
  - `err` {Error}
  - `buf` {Buffer}

生成加密强伪随机数据. `size`参数是指示要生成的字节数的数值。

如果提供 `callback`回调函数 ,这些字节是异步生成的并且使用两个参数调用`callback`函数：`err`和`buf`。
如果发生错误, `err`是一个Error对象； 否则为null。`buf`参数是包含生成字节的[`Buffer`] []。

```js
// Asynchronous
const crypto = require('crypto');
crypto.randomBytes(256, (err, buf) => {
  if (err) throw err;
  console.log(`${buf.length} bytes of random data: ${buf.toString('hex')}`);
});
```

如果未提供 `callback`回调函数, 则同步地生成随机字节并返回为[`Buffer`] []。如果生成字节遇到问题，将会抛出一个错误。
```js
// Synchronous
const buf = crypto.randomBytes(256);
console.log(
  `${buf.length} bytes of random data: ${buf.toString('hex')}`);
```

`crypto.randomBytes()`方法将在获得足够的熵之后完成。这通常不会超过几毫秒。只有在刚开机时才可能会阻塞更久，因为此时整个系统的熵不多。

注意这个API使用libuv的线程池，所以在某些时候可能会产生意外的性能问题，查看[`UV_THREADPOOL_SIZE`][]的文档以了解更多信息。
