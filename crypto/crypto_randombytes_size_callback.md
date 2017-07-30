<!-- YAML
added: v0.5.8
-->
- `size` {number}
- `callback` {Function}
  - `err` {Error}
  - `buf` {Buffer}

生成加密强伪随机数据. `size`参数是指示要生成的字节数的数字。

如果提供 `callback`回调函数 ,这些字节是异步生成的并且使用两个参数调用`callback`函数：`err`和`buf`。
如果发生错误, `err`是一个Error对象； 否则为null. 该`buf`参数是包含生成字节的[`Buffer`] []。

```js
// Asynchronous
const crypto = require('crypto');
crypto.randomBytes(256, (err, buf) => {
  if (err) throw err;
  console.log(`${buf.length} bytes of random data: ${buf.toString('hex')}`);
});
```

如果不提供 `callback`回调函数, 生成随机字节同步并返回为[`Buffer`] [].如果出现错误将会抛出生成字节有问题。
```js
// Synchronous
const buf = crypto.randomBytes(256);
console.log(
  `${buf.length} bytes of random data: ${buf.toString('hex')}`);
```

`crypto.randomBytes（）`方法将阻塞，直到有足够的熵.
这通常不会超过几毫秒. 唯一的时间
当生成随机字节可能会阻塞更长的时间
时间是开机后，当整个系统的熵低时

