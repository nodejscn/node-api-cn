<!-- YAML
added: v0.1.92
-->

* 继承自: {stream.Writable}

`Sign` 类是一个实用工具，用于生成签名。
它可以通过以下两种方式之一使用：

- 作为可写的[流][stream]，其中写入要签名的数据，并使用 [`sign.sign()`] 方法生成和返回签名。
- 使用 [`sign.update()`] 和 [`sign.sign()`] 方法生成签名。

[`crypto.createSign()`] 方法用于创建 `Sign` 实例。
参数是要使用的哈希函数的字符串名称。 
不能使用 `new` 关键字直接地创建 `Sign` 对象。

示例，使用 `Sign` 和 [`Verify`] 对象作为流：

```js
const crypto = require('crypto');

const { privateKey, publicKey } = crypto.generateKeyPairSync('ec', {
  namedCurve: 'sect239k1'
});

const sign = crypto.createSign('SHA256');
sign.write('要生成签名的数据');
sign.end();
const signature = sign.sign(privateKey, 'hex');

const verify = crypto.createVerify('SHA256');
verify.write('要生成签名的数据');
verify.end();
console.log(verify.verify(publicKey, signature, 'hex'));
// 打印 true
```

示例，使用 [`sign.update()`] 和 [`verify.update()`] 方法：

```js
const crypto = require('crypto');

const { privateKey, publicKey } = crypto.generateKeyPairSync('rsa', {
  modulusLength: 2048,
});

const sign = crypto.createSign('SHA256');
sign.update('要生成签名的数据');
sign.end();
const signature = sign.sign(privateKey);

const verify = crypto.createVerify('SHA256');
verify.update('要生成签名的数据');
verify.end();
console.log(verify.verify(publicKey, signature));
// 打印: true
```
