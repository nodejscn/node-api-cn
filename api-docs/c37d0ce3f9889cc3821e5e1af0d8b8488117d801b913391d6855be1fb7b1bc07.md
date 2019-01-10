<!-- YAML
added: v0.11.14
-->

`ECDH`类是创建椭圆曲线Diffie-Hellman（Elliptic Curve Diffie-Hellman (ECDH)）键交换的实用工具。
`ECDH`类的实例可以使用[`crypto.createECDH()`][]方法。

```js
const crypto = require('crypto');
const assert = require('assert');

// Generate Alice's keys...
const alice = crypto.createECDH('secp521r1');
const aliceKey = alice.generateKeys();

// Generate Bob's keys...
const bob = crypto.createECDH('secp521r1');
const bobKey = bob.generateKeys();

// Exchange and generate the secret...
const aliceSecret = alice.computeSecret(bobKey);
const bobSecret = bob.computeSecret(aliceKey);

assert.strictEqual(aliceSecret.toString('hex'), bobSecret.toString('hex'));
// OK
```

