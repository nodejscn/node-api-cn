<!-- YAML
added: v0.1.94
-->

* 继承自: {stream.Transform}

`Decipher` 类的实例用于解密数据。
该类可以通过以下两种方式之一使用：

- 作为可读写的[流][stream]，其中写入加密的数据以在可读侧生成未加密的数据。
- 使用 [`decipher.update()`] 和 [`decipher.final()`] 方法生成未加密的数据。

[`crypto.createDecipher()`] 或 [`crypto.createDecipheriv()`] 方法用于创建 `Decipher` 实例。
不能使用 `new` 关键字直接地创建 `Decipher` 对象。

示例，使用 `Decipher` 对象作为流：

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 密钥长度取决于算法。 
// 在此示例中，对于 aes192，它是 24 个字节（192 位）。
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, '盐值', 24);
// IV 通常与密文一起传递。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const decipher = crypto.createDecipheriv(algorithm, key, iv);

let decrypted = '';
decipher.on('readable', () => {
  while (null !== (chunk = decipher.read())) {
    decrypted += chunk.toString('utf8');
  }
});
decipher.on('end', () => {
  console.log(decrypted);
  // 打印: 要加密的数据
});

// 使用相同的算法、密钥和 iv 进行加密。
const encrypted =
  '9d47959b80d428936beef61216ef0b7653b5d23a670e082bd739f6cebcb6038f';
decipher.write(encrypted, 'hex');
decipher.end();
```

示例，使用 `Decipher` 和管道流：

```js
const crypto = require('crypto');
const fs = require('fs');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, '盐值', 24);
// IV 通常与密文一起传递。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const decipher = crypto.createDecipheriv(algorithm, key, iv);

const input = fs.createReadStream('要解密的数据.enc');
const output = fs.createWriteStream('解密后的数据.js');

input.pipe(decipher).pipe(output);
```

示例，使用 [`decipher.update()`] 和 [`decipher.final()`] 方法：

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, '盐值', 24);
// IV 通常与密文一起传递。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const decipher = crypto.createDecipheriv(algorithm, key, iv);

// 使用相同的算法、密钥和 iv 进行加密。
const encrypted =
  '9d47959b80d428936beef61216ef0b7653b5d23a670e082bd739f6cebcb6038f';
let decrypted = decipher.update(encrypted, 'hex', 'utf8');
decrypted += decipher.final('utf8');
console.log(decrypted);
// 打印: 要加密的数据
```

