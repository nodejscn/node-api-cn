<!-- YAML
added: v0.11.8
-->
* `spkac` {string | Buffer | TypedArray | DataView}
* Returns: {Buffer} The public key component of the `spkac` data structure,
  which includes a public key and a challenge.

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const publicKey = cert.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```

