<!-- YAML
added: v0.5.0
-->

`DiffieHellman` 类是一个用来创建 Diffie-Hellman 键交换的工具。

`DiffieHellman` 类的实例可以使用 [`crypto.createDiffieHellman()`][] 方法。

```js
const crypto = require('crypto');
const assert = require('assert');

// 生成 Alice 的密钥。
const alice = crypto.createDiffieHellman(2048);
const aliceKey = alice.generateKeys();

// 生成 Bob 的密钥。
const bob = crypto.createDiffieHellman(alice.getPrime(), alice.getGenerator());
const bobKey = bob.generateKeys();

// 交换并生成密钥。
const aliceSecret = alice.computeSecret(bobKey);
const bobSecret = bob.computeSecret(aliceKey);

// 完成。
assert.strictEqual(aliceSecret.toString('hex'), bobSecret.toString('hex'));
```

