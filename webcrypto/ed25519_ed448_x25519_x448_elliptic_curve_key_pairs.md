
```js
const { subtle } = require('crypto').webcrypto;

async function generateEd25519Key() {
  return subtle.generateKey({
    name: 'NODE-ED25519',
    namedCurve: 'NODE-ED25519',
  }, true, ['sign', 'verify']);
}

async function generateX25519Key() {
  return subtle.generateKey({
    name: 'ECDH',
    namedCurve: 'NODE-X25519',
  }, true, ['deriveKey']);
}
```

