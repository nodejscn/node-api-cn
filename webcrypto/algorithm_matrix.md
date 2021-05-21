
The table details the algorithms supported by the Node.js Web Crypto API
implementation and the APIs supported for each:

| Algorithm             | `generateKey` | `exportKey` | `importKey` | `encrypt` | `decrypt` | `wrapKey` | `unwrapKey` | `deriveBits` | `deriveKey` | `sign` | `verify` | `digest` |
| --------------------- | ------------- | ----------- | ----------- | --------- | --------- | --------- | ----------- | ------------ | ----------- | ------ | -------- | -------- |
| `'RSASSA-PKCS1-v1_5'` | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'RSA-PSS'`           | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'RSA-OAEP'`          | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |   |   |   |   |   |
| `'ECDSA'`             | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'ECDH'`              | ✔ | ✔ | ✔ |   |   |   |   | ✔ | ✔ |   |   |   |
| `'AES-CTR'`           | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |   |   |   |   |   |
| `'AES-CBC'`           | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |   |   |   |   |   |
| `'AES-GCM'`           | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |   |   |   |   |   |
| `'AES-KW'`            | ✔ | ✔ | ✔ |   |   | ✔ | ✔ |   |   |   |   |   |
| `'HMAC'`              | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'HKDF'`              |   | ✔ | ✔ |   |   |   |   | ✔ | ✔ |   |   |   |
| `'PBKDF2'`            |   | ✔ | ✔ |   |   |   |   | ✔ | ✔ |   |   |   |
| `'SHA-1'`             |   |   |   |   |   |   |   |   |   |   |   | ✔ |
| `'SHA-256'`           |   |   |   |   |   |   |   |   |   |   |   | ✔ |
| `'SHA-384'`           |   |   |   |   |   |   |   |   |   |   |   | ✔ |
| `'SHA-512'`           |   |   |   |   |   |   |   |   |   |   |   | ✔ |
| `'NODE-DSA'`<sup>1</sup> | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'NODE-DH'`<sup>1</sup> | ✔ | ✔ | ✔ |   |   |   |   | ✔ | ✔ |   |   |   |
| `'NODE-ED25519'`<sup>1</sup> | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |
| `'NODE-ED448'`<sup>1</sup> | ✔ | ✔ | ✔ |   |   |   |   |   |   | ✔ | ✔ |   |

<sup>1</sup> Node.js-specific extension

