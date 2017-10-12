<!-- YAML
added: v0.1.92
-->
`Verify`类是验证签名的工具。它可以两种方式使用:

- 作为可写的[stream][]，使用书面数据来验证提供的签名
- 使用[`verify.update()`][]和[`verify.verify()`][]的方法来验证签名。

[`crypto.createVerify()`][]方法用于创建`Verify`实例。
`Verify`对象不能直接使用`new`关键字创建。

示例:使用“验证”对象作为流:

```js
const crypto = require('crypto');
const verify = crypto.createVerify('SHA256');

verify.write('some data to sign');
verify.end();

const publicKey = getPublicKeySomehow();
const signature = getSignatureToVerify();
console.log(verify.verify(publicKey, signature));
// Prints: true or false
```

示例：使用[`verify.update()`][]和[`verify.verify()`][]方法

```js
const crypto = require('crypto');
const verify = crypto.createVerify('SHA256');

verify.update('some data to sign');

const publicKey = getPublicKeySomehow();
const signature = getSignatureToVerify();
console.log(verify.verify(publicKey, signature));
// Prints: true or false
```
