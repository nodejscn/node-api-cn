<!-- YAML
added: v0.1.92
-->

The `Sign` Class is a utility for generating signatures. It can be used in one
of two ways:

- As a writable [stream][], where data to be signed is written and the
  [`sign.sign()`][] method is used to generate and return the signature, or
- Using the [`sign.update()`][] and [`sign.sign()`][] methods to produce the
  signature.

The [`crypto.createSign()`][] method is used to create `Sign` instances. The
argument is the string name of the hash function to use. `Sign` objects are not
to be created directly using the `new` keyword.

Example: Using `Sign` objects as streams:

```js
const crypto = require('crypto');
const sign = crypto.createSign('SHA256');

sign.write('some data to sign');
sign.end();

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature using the specified private key and
// SHA-256. For RSA keys, the algorithm is RSASSA-PKCS1-v1_5 (see padding
// parameter below for RSASSA-PSS). For EC keys, the algorithm is ECDSA.
```

Example: Using the [`sign.update()`][] and [`sign.sign()`][] methods:

```js
const crypto = require('crypto');
const sign = crypto.createSign('SHA256');

sign.update('some data to sign');

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature
```

In some cases, a `Sign` instance can also be created by passing in a signature
algorithm name, such as 'RSA-SHA256'. This will use the corresponding digest
algorithm. This does not work for all signature algorithms, such as
'ecdsa-with-SHA256'. Use digest names instead.

Example: signing using legacy signature algorithm name

```js
const crypto = require('crypto');
const sign = crypto.createSign('RSA-SHA256');

sign.update('some data to sign');

const privateKey = getPrivateKeySomehow();
console.log(sign.sign(privateKey, 'hex'));
// Prints: the calculated signature
```
