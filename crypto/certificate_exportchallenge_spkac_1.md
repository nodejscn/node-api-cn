<!-- YAML
added: v0.11.8
-->
* `spkac` {string | Buffer | TypedArray | DataView}
* Returns: {Buffer} The challenge component of the `spkac` data structure, which
  includes a public key and a challenge.

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const challenge = cert.exportChallenge(spkac);
console.log(challenge.toString('utf8'));
// Prints: the challenge as a UTF8 string
```

