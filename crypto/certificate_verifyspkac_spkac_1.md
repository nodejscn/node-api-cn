<!-- YAML
added: v0.11.8
-->
* `spkac` {Buffer | TypedArray | DataView}
* Returns: {boolean} `true` if the given `spkac` data structure is valid,
  `false` otherwise.

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
console.log(cert.verifySpkac(Buffer.from(spkac)));
// Prints: true or false
```

