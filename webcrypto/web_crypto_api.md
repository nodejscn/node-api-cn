
<!-- introduced_in=v15.0.0 -->

> Stability: 1 - Experimental

Node.js provides an implementation of the standard [Web Crypto API][].

Use `require('crypto').webcrypto` to access this module.

```js
const { subtle } = require('crypto').webcrypto;

(async function() {

  const key = await subtle.generateKey({
    name: 'HMAC',
    hash: 'SHA-256',
    length: 256
  }, true, ['sign', 'verify']);

  const digest = await subtle.sign({
    name: 'HMAC'
  }, key, 'I love cupcakes');

})();
```

