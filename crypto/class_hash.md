<!-- YAML
added: v0.1.92
-->
`Hash`类是用于创建数据哈希值的工具类。它能用以下方法使用：
- 作为一个[stream][]，它既可读又可写，数据被写入要在可读的方面生成一个计算散列摘要

- 使用[`hash.update()`][]和[`hash.digest()`][]方法产生计算后的哈希。

[`crypto.createHash()`][]方法用于创建`Hash`实例。`Hash`不能直接使用`new`关键字创建对象。

示例: 使用`Hash`对象作为流:

```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.on('readable', () => {
  const data = hash.read();
  if (data) {
    console.log(data.toString('hex'));
    // Prints:
    //   6a2da20943931e9834fc12cfe5bb47bbd9ae43489a30726962b576f4e3993e50
  }
});

hash.write('some data to hash');
hash.end();
```
示例:使用 `Hash` 和管道流
```js
const crypto = require('crypto');
const fs = require('fs');
const hash = crypto.createHash('sha256');

const input = fs.createReadStream('test.js');
input.pipe(hash).pipe(process.stdout);
```
示例:使用[`hash.update()`][]和[`hash.digest()`][]
```js
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.update('some data to hash');
console.log(hash.digest('hex'));
// Prints:
//   6a2da20943931e9834fc12cfe5bb47bbd9ae43489a30726962b576f4e3993e50
```

