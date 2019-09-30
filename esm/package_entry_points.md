
The `package.json` `"main"` field defines the entry point for a package,
whether the package is included into CommonJS via `require` or into an ES
module via `import`.

<!-- eslint-skip -->
```js
// ./node_modules/es-module-package/package.json
{
  "type": "module",
  "main": "./src/index.js"
}
```

```js
// ./my-app.mjs

import { something } from 'es-module-package';
// Loads from ./node_modules/es-module-package/src/index.js
```

An attempt to `require` the above `es-module-package` would attempt to load
`./node_modules/es-module-package/src/index.js` as CommonJS, which would throw
an error as Node.js would not be able to parse the `export` statement in
CommonJS.

As with `import` statements, for ES module usage the value of `"main"` must be
a full path including extension: `"./index.mjs"`, not `"./index"`.

If the `package.json` `"type"` field is omitted, a `.js` file in `"main"` will
be interpreted as CommonJS.

The `"main"` field can point to exactly one file, regardless of whether the
package is referenced via `require` (in a CommonJS context) or `import` (in an
ES module context).

