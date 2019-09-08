<!-- YAML
added: v0.1.92
-->

* 继承自: {stream.Transform}

`Hash` 类是一个实用工具，用于创建数据的哈希摘要。
它可以通过以下两种方式之一使用：

- 作为可读写的[流][stream]，其中写入数据以在可读侧生成计算后的哈希摘要。
- 使用 [`hash.update()`] 和 [`hash.digest()`] 方法生成计算后的哈希。

[`crypto.createHash()`] 方法用于创建 `Hash` 实例。
不能使用 `new` 关键字直接地创建 `Hash` 对象。

示例，使用 `Hash` 对象作为流：

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.on('readable', () => {
  // 哈希流只会生成一个元素。
  const data = hash.read();
  if (data) {
    console.log(data.toString('hex'));
    // 打印:
    //   164345eba9bccbafb94b27b8299d49cc2d80627fc9995b03230965e6d8bcbf56
  }
});

hash.write('要创建哈希摘要的数据');
hash.end();
```

示例，使用 `Hash` 和管道流：

```js
const crypto = require('crypto');
const fs = require('fs');
const hash = crypto.createHash('sha256');

const input = fs.createReadStream('要创建哈希摘要的数据.txt');
input.pipe(hash).pipe(process.stdout);
```

示例，使用 [`hash.update()`] 和 [`hash.digest()`] 方法：

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.update('要创建哈希摘要的数据');
console.log(hash.digest('hex'));
// 打印:
//   164345eba9bccbafb94b27b8299d49cc2d80627fc9995b03230965e6d8bcbf56
```

