<!-- YAML
added: v0.1.94
-->

`Cipher`类的实例用于加密数据。这个类可以用在以下两种方法中的一种:

- 作为[stream][]，既可读又可写，未加密数据的编写是为了在可读的方面生成加密的数据，或者
- 使用[`cipher.update()`][]和[`cipher.final()`][]方法产生加密的数据。

[`crypto.createCipher()`][]或[`crypto.createCipheriv()`][]方法用于创建`Cipher`实例。`Cipher`对象不能直接使用`new`关键字创建。

示例:使用`Cipher`对象作为流:

```js
const crypto = require('crypto');
const cipher = crypto.createCipher('aes192', 'a password');

let encrypted = '';
cipher.on('readable', () => {
  const data = cipher.read();
  if (data)
    encrypted += data.toString('hex');
});
cipher.on('end', () => {
  console.log(encrypted);
  // Prints: ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504
});

cipher.write('some clear text data');
cipher.end();
```

示例:使用`Cipher`和管道流:

```js
const crypto = require('crypto');
const fs = require('fs');
const cipher = crypto.createCipher('aes192', 'a password');

const input = fs.createReadStream('test.js');
const output = fs.createWriteStream('test.enc');

input.pipe(cipher).pipe(output);
```

示例:使用[`cipher.update()`][]和[`cipher.final()`][]方法:

```js
const crypto = require('crypto');
const cipher = crypto.createCipher('aes192', 'a password');

let encrypted = cipher.update('some clear text data', 'utf8', 'hex');
encrypted += cipher.final('hex');
console.log(encrypted);
// Prints: ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504
```

