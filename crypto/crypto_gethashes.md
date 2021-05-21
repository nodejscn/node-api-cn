<!-- YAML
added: v0.9.3
-->

* Returns: {string[]} An array of the names of the supported hash algorithms,
  such as `'RSA-SHA256'`. Hash algorithms are also called "digest" algorithms.

```mjs
const {
  getHashes,
} = await import('crypto');

console.log(getHashes()); // ['DSA', 'DSA-SHA', 'DSA-SHA1', ...]
```

```cjs
const {
  getHashes,
} = require('crypto');

console.log(getHashes()); // ['DSA', 'DSA-SHA', 'DSA-SHA1', ...]
```

