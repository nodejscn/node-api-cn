<!-- YAML
added: v0.1.94
-->

`Decipher`类的实例用于解密数据。这个类可以用在以下两种方法中的一种:

- 作为[stream][]，既可读，又可写，加密数据的编写是为了在可读的方面生成未加密的数据
- 使用[`decipher.update()`][]和[`decipher.final()`][]方法产生未加密的数据。

[`crypto.createDecipher()`][]或[`crypto.createDecipheriv()`][]的方法
用于创建`Decipher`实例。`Decipher`对象不能直接使用`new`关键字创建。

示例:使用`Decipher`对象作为流:

```js
const crypto = require('crypto');
const decipher = crypto.createDecipher('aes192', 'a password');

let decrypted = '';
decipher.on('readable', () => {
  const data = decipher.read();
  if (data)
    decrypted += data.toString('utf8');
});
decipher.on('end', () => {
  console.log(decrypted);
  // Prints: some clear text data
});

const encrypted =
    'ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504';
decipher.write(encrypted, 'hex');
decipher.end();
```

示例:使用`Decipher`和管道流:

```js
const crypto = require('crypto');
const fs = require('fs');
const decipher = crypto.createDecipher('aes192', 'a password');

const input = fs.createReadStream('test.enc');
const output = fs.createWriteStream('test.js');

input.pipe(decipher).pipe(output);
```

示例:使用[`decipher.update()`][]和[`decipher.final()`][]方法:

```js
const crypto = require('crypto');
const decipher = crypto.createDecipher('aes192', 'a password');

const encrypted =
    'ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504';
let decrypted = decipher.update(encrypted, 'hex', 'utf8');
decrypted += decipher.final('utf8');
console.log(decrypted);
// Prints: some clear text data
```

