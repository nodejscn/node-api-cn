<!-- YAML
added: v0.5.0
-->

The `DiffieHellman` class is a utility for creating Diffie-Hellman key
exchanges.

Instances of the `DiffieHellman` class can be created using the
[`crypto.createDiffieHellman()`][] function.

```js
const crypto = require('crypto');
const assert = require('assert');

// Generate Alice's keys...
const alice = crypto.createDiffieHellman(2048);
const alice_key = alice.generateKeys();

// Generate Bob's keys...
const bob = crypto.createDiffieHellman(alice.getPrime(), alice.getGenerator());
const bob_key = bob.generateKeys();

// Exchange and generate the secret...
const alice_secret = alice.computeSecret(bob_key);
const bob_secret = bob.computeSecret(alice_key);

// OK
assert.equal(alice_secret.toString('hex'), bob_secret.toString('hex'));
```

