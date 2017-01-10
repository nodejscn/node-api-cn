<!-- YAML
added: v0.11.8
-->

The `spkac` data structure includes a public key and a challenge. The
`certificate.exportChallenge()` returns the challenge component in the
form of a Node.js [`Buffer`][]. The `spkac` argument can be either a string
or a [`Buffer`][].

```js
const cert = require('crypto').Certificate();
const spkac = getSpkacSomehow();
const challenge = cert.exportChallenge(spkac);
console.log(challenge.toString('utf8'));
// Prints: the challenge as a UTF8 string
```

