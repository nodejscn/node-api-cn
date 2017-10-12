<!-- YAML
added: v0.1.92
-->

“Sign”类是生成签名的实用工具。它有两种使用方式:

- 作为一个可写的[stream][]，在这里，要签署的数据是写出来的，[`sign.sign()`][]方法用于生成并返回签名
- 使用[`sign.update()`][]和[`sign.sign()`][]方法生产签名。

[`crypto.createSign()`][]方法用于创建`Sign`实例。`Sign`实例不能直接使用`new`关键字创建。

示例:使用“符号”对象作为流:

```js
const crypto = require('crypto');
const sign = crypto.createSign('SHA256');

sign.write('some data to sign');
sign.end();

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature using the specified private key and
// SHA-256. For RSA keys, the algorithm is RSASSA-PKCS1-v1_5 (see padding
// parameter below for RSASSA-PSS). For EC keys, the algorithm is ECDSA.
```

示例：使用[`sign.update()`][]和[`sign.sign()`][]方法：

```js
const crypto = require('crypto');
const sign = crypto.createSign('SHA256');

sign.update('some data to sign');

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature
```

一个`Sign`实例也可以通过仅仅通过摘要来创建算法名称，在这种情况下，OpenSSL将会从PEM-formatted私钥的类型推断出完整的签名算法，包括不直接暴露姓名常数的算法。比如'ecdsa-with-SHA256'。

示例:使用ECDSA与SHA256进行签名

```js
const crypto = require('crypto');
const sign = crypto.createSign('RSA-SHA256');

sign.update('some data to sign');

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature
```
