<!-- YAML
added: v0.11.14
-->

The `ECDH` class is a utility for creating Elliptic Curve Diffie-Hellman (ECDH)
key exchanges.

Instances of the `ECDH` class can be created using the
[`crypto.createECDH()`][] function.

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

