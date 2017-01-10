<!-- YAML
added: v0.1.92
-->

The `Sign` Class is a utility for generating signatures. It can be used in one
of two ways:

- As a writable [stream][], where data to be signed is written and the
  [`sign.sign()`][] method is used to generate and return the signature, or
- Using the [`sign.update()`][] and [`sign.sign()`][] methods to produce the
  signature.

The [`crypto.createSign()`][] method is used to create `Sign` instances. `Sign`
objects are not to be created directly using the `new` keyword.

Example: Using `Sign` objects as streams:

```js
const crypto = require('crypto');
const sign = crypto.createSign('RSA-SHA256');

sign.write('some data to sign');
sign.end();

const private_key = getPrivateKeySomehow();
console.log(sign.sign(private_key, 'hex'));
// Prints: the calculated signature
```

Example: Using the [`sign.update()`][] and [`sign.sign()`][] methods:

```js
const crypto = require('crypto');
const sign = crypto.createSign('RSA-SHA256');

sign.update('some data to sign');

const private_key = getPrivateKeySomehow();
console.log(sign.sign(private_key, 'hex'));
// Prints: the calculated signature
```

A `Sign` instance can also be created by just passing in the digest
algorithm name, in which case OpenSSL will infer the full signature algorithm
from the type of the PEM-formatted private key, including algorithms that
do not have directly exposed name constants, e.g. 'ecdsa-with-SHA256'.

Example: signing using ECDSA with SHA256

```js
const crypto = require('crypto');
const sign = crypto.createSign('sha256');

sign.update('some data to sign');

const private_key = '-----BEGIN EC PRIVATE KEY-----\n' +
        'MHcCAQEEIF+jnWY1D5kbVYDNvxxo/Y+ku2uJPDwS0r/VuPZQrjjVoAoGCCqGSM49\n' +
        'AwEHoUQDQgAEurOxfSxmqIRYzJVagdZfMMSjRNNhB8i3mXyIMq704m2m52FdfKZ2\n' +
        'pQhByd5eyj3lgZ7m7jbchtdgyOF8Io/1ng==\n' +
        '-----END EC PRIVATE KEY-----\n';

console.log(sign.sign(private_key).toString('hex'));
```

