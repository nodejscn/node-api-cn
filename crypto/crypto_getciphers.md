<!-- YAML
added: v0.9.3
-->

* Returns: {string[]} An array with the names of the supported cipher
  algorithms.

```mjs
const {
  getCiphers,
} = await import('crypto');

console.log(getCiphers()); // ['aes-128-cbc', 'aes-128-ccm', ...]
```

```cjs
const {
  getCiphers,
} = require('crypto');

console.log(getCiphers()); // ['aes-128-cbc', 'aes-128-ccm', ...]
```

