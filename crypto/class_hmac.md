<!-- YAML
added: v0.1.94
-->

* 继承自: {stream.Transform}

`Hmac` 类是一个实用工具，用于创建加密的 HMAC 摘要。
它可以通过以下两种方式之一使用：


- 作为可读写的[流][stream]，其中写入数据以在可读侧生成计算后的 HMAC 摘要。
- 使用 [`hmac.update()`] 和 [`hmac.digest()`] 方法生成计算后的 HMAC 摘要。

[`crypto.createHmac()`] 方法用于创建 `Hmac` 实例。
不能使用 `new` 关键字直接地创建 `Hmac` 对象。

示例，使用 `Hmac` 对象作为流：

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', '密钥');

hmac.on('readable', () => {
  // 哈希流只会生成一个元素。
  const data = hmac.read();
  if (data) {
    console.log(data.toString('hex'));
    // 打印:
    //   d0b5490ab4beb8e6545fe284f484d0d595e46086cb8e6ef2291af12ac684102f
  }
});

hmac.write('要创建哈希的数据');
hmac.end();
```

示例，使用 `Hmac` 和管道流：

```js
const crypto = require('crypto');
const fs = require('fs');
const hmac = crypto.createHmac('sha256', '密钥');

const input = fs.createReadStream('要创建哈希的数据.txt');
input.pipe(hmac).pipe(process.stdout);
```

示例，使用 [`hmac.update()`] 和 [`hmac.digest()`] 方法：

```js
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', '密钥');

hmac.update('要创建哈希的数据');
console.log(hmac.digest('hex'));
// 打印:
//   d0b5490ab4beb8e6545fe284f484d0d595e46086cb8e6ef2291af12ac684102f
```

