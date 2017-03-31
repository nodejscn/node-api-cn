<!-- YAML
added: v0.1.92
-->

The `Verify` class is a utility for verifying signatures. It can be used in one
of two ways:

- As a writable [stream][] where written data is used to validate against the
  supplied signature, or
- Using the [`verify.update()`][] and [`verify.verify()`][] methods to verify
  the signature.

The [`crypto.createVerify()`][] method is used to create `Verify` instances.
`Verify` objects are not to be created directly using the `new` keyword.

Example: Using `Verify` objects as streams:

```js
const crypto = require('crypto');
const verify = crypto.createVerify('RSA-SHA256');

verify.write('some data to sign');
verify.end();

const publicKey = getPublicKeySomehow();
const signature = getSignatureToVerify();
console.log(verify.verify(publicKey, signature));
// Prints: true or false
```

Example: Using the [`verify.update()`][] and [`verify.verify()`][] methods:

```js
const crypto = require('crypto');
const verify = crypto.createVerify('RSA-SHA256');

verify.update('some data to sign');

const publicKey = getPublicKeySomehow();
const signature = getSignatureToVerify();
console.log(verify.verify(publicKey, signature));
// Prints: true or false
```

