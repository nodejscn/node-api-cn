
Within a package, the values defined in the package’s
`package.json` `"exports"` field can be referenced via the package’s name.
For example, assuming the `package.json` is:

```json
// package.json
{
  "name": "a-package",
  "exports": {
    ".": "./main.mjs",
    "./foo": "./foo.js"
  }
}
```

Then any module _in that package_ can reference an export in the package itself:

```js
// ./a-module.mjs
import { something } from 'a-package'; // Imports "something" from ./main.mjs.
```

Self-referencing is available only if `package.json` has `exports`, and will
allow importing only what that `exports` (in the `package.json`) allows.
So the code below, given the previous package, will generate a runtime error:

```js
// ./another-module.mjs

// Imports "another" from ./m.mjs. Fails because
// the "package.json" "exports" field
// does not provide an export named "./m.mjs".
import { another } from 'a-package/m.mjs';
```

Self-referencing is also available when using `require`, both in an ES module,
and in a CommonJS one. For example, this code will also work:

```js
// ./a-module.js
const { something } = require('a-package/foo'); // Loads from ./foo.js.
```

