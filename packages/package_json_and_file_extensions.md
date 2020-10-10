
Within a package, the [`package.json`][] [`"type"`][] field defines how
Node.js should interpret `.js` files. If a `package.json` file does not have a
`"type"` field, `.js` files are treated as [CommonJS][].

A `package.json` `"type"` value of `"module"` tells Node.js to interpret `.js`
files within that package as using [ES module][] syntax.

The `"type"` field applies not only to initial entry points (`node my-app.js`)
but also to files referenced by `import` statements and `import()` expressions.

```js
// my-app.js, treated as an ES module because there is a package.json
// file in the same folder with "type": "module".

import './startup/init.js';
// Loaded as ES module since ./startup contains no package.json file,
// and therefore inherits the "type" value from one level up.

import 'commonjs-package';
// Loaded as CommonJS since ./node_modules/commonjs-package/package.json
// lacks a "type" field or contains "type": "commonjs".

import './node_modules/commonjs-package/index.js';
// Loaded as CommonJS since ./node_modules/commonjs-package/package.json
// lacks a "type" field or contains "type": "commonjs".
```

Files ending with `.mjs` are always loaded as [ES modules][] regardless of
the nearest parent `package.json`.

Files ending with `.cjs` are always loaded as [CommonJS][] regardless of the
nearest parent `package.json`.

```js
import './legacy-file.cjs';
// Loaded as CommonJS since .cjs is always loaded as CommonJS.

import 'commonjs-package/src/index.mjs';
// Loaded as ES module since .mjs is always loaded as ES module.
```

The `.mjs` and `.cjs` extensions can be used to mix types within the same
package:

* Within a `"type": "module"` package, Node.js can be instructed to
  interpret a particular file as [CommonJS][] by naming it with a `.cjs`
  extension (since both `.js` and `.mjs` files are treated as ES modules within
  a `"module"` package).

* Within a `"type": "commonjs"` package, Node.js can be instructed to
  interpret a particular file as an [ES module][] by naming it with an `.mjs`
  extension (since both `.js` and `.cjs` files are treated as CommonJS within a
  `"commonjs"` package).

