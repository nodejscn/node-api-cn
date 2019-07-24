
CommonJS, JSON, and Native modules can be used with
[`module.createRequire()`][].

```js
// cjs.js
module.exports = 'cjs';

// esm.mjs
import { createRequire } from 'module';
import { fileURLToPath as fromURL } from 'url';

const require = createRequire(fromURL(import.meta.url));

const cjs = require('./cjs');
cjs === 'cjs'; // true
```

