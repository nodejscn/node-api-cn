<!-- YAML
added: v0.11.14
deprecated: v5.2.0
-->

> Stability: 0 - Deprecated

- `publicKey` {string | Buffer | TypedArray | DataView}
- `encoding` {string}

Sets the EC Diffie-Hellman public key. Key encoding can be `'latin1'`,
`'hex'` or `'base64'`. If `encoding` is provided `publicKey` is expected to
be a string; otherwise a [`Buffer`][], `TypedArray`, or `DataView` is expected.

Note that there is not normally a reason to call this method because `ECDH`
only requires a private key and the other party's public key to compute the
shared secret. Typically either [`ecdh.generateKeys()`][] or
[`ecdh.setPrivateKey()`][] will be called. The [`ecdh.setPrivateKey()`][] method
attempts to generate the public point/key associated with the private key being
set.

Example (obtaining a shared secret):

```js
const crypto = require('crypto');
const alice = crypto.createECDH('secp256k1');
const bob = crypto.createECDH('secp256k1');

// Note: This is a shortcut way to specify one of Alice's previous private
// keys. It would be unwise to use such a predictable private key in a real
// application.
alice.setPrivateKey(
  crypto.createHash('sha256').update('alice', 'utf8').digest()
);

// Bob uses a newly generated cryptographically strong
// pseudorandom key pair
bob.generateKeys();

const aliceSecret = alice.computeSecret(bob.getPublicKey(), null, 'hex');
const bobSecret = bob.computeSecret(alice.getPublicKey(), null, 'hex');

// aliceSecret and bobSecret should be the same shared secret value
console.log(aliceSecret === bobSecret);
```

