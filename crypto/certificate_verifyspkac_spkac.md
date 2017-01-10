<!-- YAML
added: v0.11.8
-->

Returns `true` if the given `spkac` data structure is valid, `false` otherwise.
The `spkac` argument must be a Node.js [`Buffer`][].

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
console.log(cert.verifySpkac(Buffer.from(spkac)));
// Prints: true or false
```

