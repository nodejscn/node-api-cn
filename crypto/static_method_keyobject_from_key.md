<!-- YAML
added: v15.0.0
-->

* `key` {CryptoKey}
* Returns: {KeyObject}

Example: Converting a `CryptoKey` instance to a `KeyObject`:

```mjs
const {
  webcrypto: {
    subtle,
  },
  KeyObject,
} = await import('crypto');

const key = await subtle.generateKey({
  name: 'HMAC',
  hash: 'SHA-256',
  length: 256
}, true, ['sign', 'verify']);

const keyObject = KeyObject.from(key);
console.log(keyObject.symmetricKeySize);
// Prints: 32 (symmetric key size in bytes)
```

```cjs
const {
  webcrypto: {
    subtle,
  },
  KeyObject,
} = require('crypto');

(async function() {
  const key = await subtle.generateKey({
    name: 'HMAC',
    hash: 'SHA-256',
    length: 256
  }, true, ['sign', 'verify']);

  const keyObject = KeyObject.from(key);
  console.log(keyObject.symmetricKeySize);
  // Prints: 32 (symmetric key size in bytes)
})();
```

