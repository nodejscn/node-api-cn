<!-- YAML
added: v0.1.94
-->
`Hmac`类是用于创建加密Hmac摘要的工具。它可以有两种用法:
- 作为[stream][],它既可读又可写，数据被写入要在可读的方面生成一个经过计算的HMAC摘要。
- 使用[`hmac.update()`][]和[`hmac.digest()`][]方法产生计算后的HMAC摘要。

[`crypto.createHmac()`][]方法用来创建`Hmac`实例。`Hmac`不能直接使用`new`关键字创建对象。

示例:使用`Hmac`对象作为流:

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', 'a secret');

hmac.on('readable', () => {
  const data = hmac.read();
  if (data) {
    console.log(data.toString('hex'));
    // Prints:
    //   7fd04df92f636fd450bc841c9418e5825c17f33ad9c87c518115a45971f7f77e
  }
});

hmac.write('some data to hash');
hmac.end();
```

示例：使用`Hmac`和管道流

```js
const crypto = require('crypto');
const fs = require('fs');
const hmac = crypto.createHmac('sha256', 'a secret');

const input = fs.createReadStream('test.js');
input.pipe(hmac).pipe(process.stdout);
```

示例：使用[`hmac.update()`][]和[`hmac.digest()`][]方法

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', 'a secret');

hmac.update('some data to hash');
console.log(hmac.digest('hex'));
// Prints:
//   7fd04df92f636fd450bc841c9418e5825c17f33ad9c87c518115a45971f7f77e
```

