
JSON imports are still experimental and only supported via the
`--experimental-json-modules` flag.

Local JSON files can be loaded relative to `import.meta.url` with `fs` directly:

<!-- eslint-skip -->
```js
import { readFile } from 'fs/promises';
const json = JSON.parse(await readFile(new URL('./dat.json', import.meta.url)));
```

Alternatively `module.createRequire()` can be used.

