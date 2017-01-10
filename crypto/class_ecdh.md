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
const alice_key = alice.generateKeys();

// Generate Bob's keys...
const bob = crypto.createECDH('secp521r1');
const bob_key = bob.generateKeys();

// Exchange and generate the secret...
const alice_secret = alice.computeSecret(bob_key);
const bob_secret = bob.computeSecret(alice_key);

assert(alice_secret, bob_secret);
  // OK
```

