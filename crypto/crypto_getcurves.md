<!-- YAML
added: v2.3.0
-->

* Returns: {string[]} An array with the names of the supported elliptic curves.

```mjs
const {
  getCurves,
} = await import('crypto');

console.log(getCurves()); // ['Oakley-EC2N-3', 'Oakley-EC2N-4', ...]
```

```cjs
const {
  getCurves,
} = require('crypto');

console.log(getCurves()); // ['Oakley-EC2N-3', 'Oakley-EC2N-4', ...]
```

