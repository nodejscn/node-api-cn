<!-- YAML
added: v0.1.94
-->

* 继承自: {stream.Transform}

`Cipher` 类的实例用于加密数据。
该类可以通过以下两种方式之一使用：

- 作为可读写的[流][stream]，其中写入未加密的数据以在可读侧生成加密的数据。
- 使用 [`cipher.update()`] 和 [`cipher.final()`] 方法生成加密的数据。

[`crypto.createCipher()`] 或 [`crypto.createCipheriv()`] 方法用于创建 `Cipher` 实例。
不能使用 `new` 关键字直接地创建 `Cipher` 对象。

示例，使用 `Cipher` 对象作为流：

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 密钥长度取决于算法。 
// 在此示例中，对于 aes192，它是 24 个字节（192 位）。
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机的 iv 而不是此处显示的静态的 iv。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const cipher = crypto.createCipheriv(algorithm, key, iv);

let encrypted = '';
cipher.on('readable', () => {
  let chunk;
  while (null !== (chunk = cipher.read())) {
    encrypted += chunk.toString('hex');
  }
});
cipher.on('end', () => {
  console.log(encrypted);
  // 打印: 3accbdcaf5574941a9c879da51711ffc2a5a017757fa736eacc579b9088ba712
});

cipher.write('要加密的数据');
cipher.end();
```

示例，使用 `Cipher` 和管道流：

```js
const crypto = require('crypto');
const fs = require('fs');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机的 iv 而不是此处显示的静态的 iv。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const cipher = crypto.createCipheriv(algorithm, key, iv);

const input = fs.createReadStream('要加密的数据.txt');
const output = fs.createWriteStream('加密后的数据.enc');

input.pipe(cipher).pipe(output);
```

示例，使用 [`cipher.update()`] 和 [`cipher.final()`] 方法:

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = '用于生成密钥的密码';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机的 iv 而不是此处显示的静态的 iv。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const cipher = crypto.createCipheriv(algorithm, key, iv);

let encrypted = cipher.update('要加密的数据', 'utf8', 'hex');
encrypted += cipher.final('hex');
console.log(encrypted);
// 打印: 3accbdcaf5574941a9c879da51711ffc2a5a017757fa736eacc579b9088ba712
```

