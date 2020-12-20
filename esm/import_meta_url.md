
* {string} The absolute `file:` URL of the module.

This is defined exactly the same as it is in browsers providing the URL of the
current module file.

This enables useful patterns such as relative file loading:

```js
import { readFileSync } from 'fs';
const buffer = readFileSync(new URL('./data.proto', import.meta.url));
```

