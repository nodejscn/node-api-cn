<!-- YAML
added: v0.11.14
-->

`ECDH` 类是创建椭圆曲线 Elliptic Curve Diffie-Hellman（ECDH）键交换的实用工具。

`ECDH` 类的实例可以使用 [`crypto.createECDH()`][] 方法。

```js
const crypto = require('crypto');
const assert = require('assert');

// 生成 Alice 的密钥。
const alice = crypto.createECDH('secp521r1');
const aliceKey = alice.generateKeys();

// 生成 Bob 的密钥。
const bob = crypto.createECDH('secp521r1');
const bobKey = bob.generateKeys();

// 交换并生成密钥。
const aliceSecret = alice.computeSecret(bobKey);
const bobSecret = bob.computeSecret(aliceKey);

assert.strictEqual(aliceSecret.toString('hex'), bobSecret.toString('hex'));
// 完成
```

