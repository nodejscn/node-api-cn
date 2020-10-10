<!-- YAML
added: v0.5.8
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/16454
    description: Passing `null` as the `callback` argument now throws
                 `ERR_INVALID_CALLBACK`.
-->
* `size` {number}
* `callback` {Function}
  - `err` {Error}
  - `buf` {Buffer}
* 返回: {Buffer} 如果未提供 `callback` 函数。

生成加密强伪随机数据。
`size` 参数是指示要生成的字节数的数值。

如果提供 `callback` 函数，则这些字节是异步生成的并且使用两个参数调用 `callback` 函数：`err` 和 `buf`。
如果发生错误，则 `err` 是一个 `Error` 对象，否则为 `null`。
`buf` 参数是包含生成字节的 [`Buffer`]。

```js
// 异步的。
const crypto = require('crypto');
crypto.randomBytes(256, (err, buf) => {
  if (err) throw err;
  console.log(`${buf.length} 位的随机数据: ${buf.toString('hex')}`);
});
```

如果未提供 `callback` 函数，则同步地生成随机字节并返回为 [`Buffer`]。
如果生成字节遇到问题，将会抛出一个错误。

```js
// 同步的。
const buf = crypto.randomBytes(256);
console.log(
  `${buf.length} 位的随机数据: ${buf.toString('hex')}`);
```

`crypto.randomBytes()` 方法将在获得足够的熵之后完成。
这通常不会超过几毫秒。
只有在刚开启时才可能会阻塞更久，因为此时整个系统的熵不多。

这个 API 使用 libuv 的线程池，所以在某些时候可能会产生意外的性能问题，查看 [`UV_THREADPOOL_SIZE`] 的文档以了解更多信息。

`crypto.randomBytes()` 的异步版本在单个线程池请求中执行。 
要最小化线程池任务长度变化，请在执行此操作时对大型的 `randomBytes` 请求进行分区，以完成客户端请求。


