<!-- YAML
added: v0.1.92
-->

`Sign` 类是生成签名的实用工具。它有两种使用方式:

- 作为一个[可写流][stream]，写入要签名的数据，并使用 [`sign.sign()`][] 方法生成并返回签名。
- 使用 [`sign.update()`][] 和 [`sign.sign()`][] 方法生产签名。

[`crypto.createSign()`][] 方法用于创建 `Sign` 实例，参数为即将用来生成 hash 值的函数名。
`Sign` 实例不能直接使用 `new` 关键字创建。

示例，像使用流对象一样使用 `Sign` 和 [`Verify`] 对象:

```js
const crypto = require('crypto');

const { privateKey, publicKey } = crypto.generateKeyPairSync('ec', {
  namedCurve: 'sect239k1'
});

const sign = crypto.createSign('SHA256');
sign.write('some data to sign');
sign.end();
const signature = sign.sign(privateKey, 'hex');

const verify = crypto.createVerify('SHA256');
verify.write('some data to sign');
verify.end();
console.log(verify.verify(publicKey, signature));
// 打印 true 或 false。
```

示例，使用 [`sign.update()`][] 和 [`sign.sign()`][] 方法：

```js
const crypto = require('crypto');

const { privateKey, publicKey } = crypto.generateKeyPairSync('rsa', {
  modulusLength: 2048,
});

const sign = crypto.createSign('SHA256');
sign.update('some data to sign');
sign.end();
const signature = sign.sign(privateKey);

const verify = crypto.createVerify('SHA256');
verify.update('some data to sign');
verify.end();
console.log(verify.verify(publicKey, signature));
// 打印: true
```
