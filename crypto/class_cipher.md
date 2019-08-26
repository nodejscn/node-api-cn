<!-- YAML
added: v0.1.94
-->

`Cipher` 类的实例用于加密数据。
这个类可以用在以下两种方法中的一种:

- 作为[流][stream]，既可读又可写，未加密数据的编写是为了在可读的方面生成加密的数据。
- 使用 [`cipher.update()`][] 和 [`cipher.final()`][] 方法产生加密的数据。

[`crypto.createCipher()`][] 或 [`crypto.createCipheriv()`][] 方法用于创建 `Cipher` 实例。
`Cipher` 对象不能直接使用 `new` 关键字创建。

示例，使用` Cipher` 对象作为流:

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 密钥长度取决于算法。 
// 在这种情况下，对于 aes192，它是 24 字节（192 位）。
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机 iv 而不是此处显示的静态 iv。
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
  // 打印: e5f79c5915c02171eec6b212d5520d44480993d7d622a7c4c2da32f6efda0ffa
});

cipher.write('some clear text data');
cipher.end();
```

示例，使用 `Cipher` 和管道流:

```js
const crypto = require('crypto');
const fs = require('fs');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机 iv 而不是此处显示的静态 iv。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const cipher = crypto.createCipheriv(algorithm, key, iv);

const input = fs.createReadStream('test.js');
const output = fs.createWriteStream('test.enc');

input.pipe(cipher).pipe(output);
```

示例，使用 [`cipher.update()`][] 和 [`cipher.final()`][] 方法:

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// 使用 `crypto.randomBytes()` 生成随机 iv 而不是此处显示的静态 iv。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const cipher = crypto.createCipheriv(algorithm, key, iv);

let encrypted = cipher.update('some clear text data', 'utf8', 'hex');
encrypted += cipher.final('hex');
console.log(encrypted);
// 打印: e5f79c5915c02171eec6b212d5520d44480993d7d622a7c4c2da32f6efda0ffa
```

