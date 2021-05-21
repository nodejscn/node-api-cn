<!-- YAML
added: v9.0.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The spkac argument can be an ArrayBuffer. Limited the size of
                 the spkac argument to a maximum of 2**31 - 1 bytes.
-->

* `spkac` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* `encoding` {string} The [encoding][] of the `spkac` string.
* Returns: {Buffer} The public key component of the `spkac` data structure,
  which includes a public key and a challenge.

```mjs
const { Certificate } = await import('crypto');
const spkac = getSpkacSomehow();
const publicKey = Certificate.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```

```cjs
const { Certificate } = require('crypto');
const spkac = getSpkacSomehow();
const publicKey = Certificate.exportPublicKey(spkac);
console.log(publicKey);
// Prints: the public key as <Buffer ...>
```

