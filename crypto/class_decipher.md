<!-- YAML
added: v0.1.94
-->

`Decipher` 类的实例用于解密数据。这个类可以用在以下两种方法中的一种:

- 作为[流][stream]，既可读又可写，加密数据的编写是为了在可读的方面生成未加密的数据。
- 使用 [`decipher.update()`][] 和 [`decipher.final()`][] 方法产生未加密的数据。

[`crypto.createDecipher()`][] 或 [`crypto.createDecipheriv()`][] 的方法用于创建`Decipher`实例。
`Decipher` 对象不能直接使用 `new` 关键字创建。

示例，使用 `Decipher` 对象作为流：

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 密钥长度取决于算法。 
// 在这种情况下，对于 aes192，它是 24 字节（192 位）。
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
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
  // 打印: some clear text data
});

// 使用相同的算法，密钥和 iv 加密。
const encrypted =
  'e5f79c5915c02171eec6b212d5520d44480993d7d622a7c4c2da32f6efda0ffa';
decipher.write(encrypted, 'hex');
decipher.end();
```

示例，使用 `Decipher` 和管道流：

```js
const crypto = require('crypto');
const fs = require('fs');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// IV 通常与密文一起传递。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const decipher = crypto.createDecipheriv(algorithm, key, iv);

const input = fs.createReadStream('test.enc');
const output = fs.createWriteStream('test.js');

input.pipe(decipher).pipe(output);
```

示例，使用 [`decipher.update()`][] 和 [`decipher.final()`][] 方法：

```js
const crypto = require('crypto');

const algorithm = 'aes-192-cbc';
const password = 'Password used to generate key';
// 改为使用异步的 `crypto.scrypt()`。
const key = crypto.scryptSync(password, 'salt', 24);
// IV 通常与密文一起传递。
const iv = Buffer.alloc(16, 0); // 初始化向量。

const decipher = crypto.createDecipheriv(algorithm, key, iv);

// 使用相同的算法，密钥和 iv 加密。
const encrypted =
  'e5f79c5915c02171eec6b212d5520d44480993d7d622a7c4c2da32f6efda0ffa';
let decrypted = decipher.update(encrypted, 'hex', 'utf8');
decrypted += decipher.final('utf8');
console.log(decrypted);
// 打印: some clear text data
```

