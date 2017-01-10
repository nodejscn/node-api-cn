<!-- YAML
added: v0.11.8
-->

The `spkac` data structure includes a public key and a challenge. The
`certificate.exportPublicKey()` returns the public key component in the
form of a Node.js [`Buffer`][]. The `spkac` argument can be either a string
or a [`Buffer`][].

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const publicKey = cert.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```

