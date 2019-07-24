<!-- YAML
added: v9.0.0
-->
* `spkac` {string | Buffer | TypedArray | DataView}
* `encoding` {string} The [encoding][] of the `spkac` string.
* Returns: {Buffer} The public key component of the `spkac` data structure,
  which includes a public key and a challenge.

```js
const { Certificate } = require('crypto');
const spkac = getSpkacSomehow();
const publicKey = Certificate.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```

