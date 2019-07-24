<!-- YAML
added: v10.0.0
-->

* `key` {string | Buffer | TypedArray | DataView}
* `curve` {string}
* `inputEncoding` {string} The [encoding][] of the `key` string.
* `outputEncoding` {string} The [encoding][] of the return value.
* `format` {string} **Default:** `'uncompressed'`
* Returns: {Buffer | string}

Converts the EC Diffie-Hellman public key specified by `key` and `curve` to the
format specified by `format`. The `format` argument specifies point encoding
and can be `'compressed'`, `'uncompressed'` or `'hybrid'`. The supplied key is
interpreted using the specified `inputEncoding`, and the returned key is encoded
using the specified `outputEncoding`.

Use [`crypto.getCurves()`][] to obtain a list of available curve names.
On recent OpenSSL releases, `openssl ecparam -list_curves` will also display
the name and description of each available elliptic curve.

If `format` is not specified the point will be returned in `'uncompressed'`
format.

If the `inputEncoding` is not provided, `key` is expected to be a [`Buffer`][],
`TypedArray`, or `DataView`.

Example (uncompressing a key):

```js
const { createECDH, ECDH } = require('crypto');

const ecdh = createECDH('secp256k1');
ecdh.generateKeys();

const compressedKey = ecdh.getPublicKey('hex', 'compressed');

const uncompressedKey = ECDH.convertKey(compressedKey,
                                        'secp256k1',
                                        'hex',
                                        'hex',
                                        'uncompressed');

// the converted key and the uncompressed public key should be the same
console.log(uncompressedKey === ecdh.getPublicKey('hex'));
```

