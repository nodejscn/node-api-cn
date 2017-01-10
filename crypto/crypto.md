
> Stability: 2 - Stable

The `crypto` module provides cryptographic functionality that includes a set of
wrappers for OpenSSL's hash, HMAC, cipher, decipher, sign and verify functions.

Use `require('crypto')` to access this module.

```js
const crypto = require('crypto');

const secret = 'abcdefg';
const hash = crypto.createHmac('sha256', secret)
                   .update('I love cupcakes')
                   .digest('hex');
console.log(hash);
// Prints:
//   c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e
```

