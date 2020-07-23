
A folder containing a `package.json` file, and all subfolders below that folder
until the next folder containing another `package.json`, are a
_package scope_. The `"type"` field defines how to treat `.js` files
within the package scope. Every package in a
project’s `node_modules` folder contains its own `package.json` file, so each
project’s dependencies have their own package scopes. If a `package.json` file
does not have a `"type"` field, the default `"type"` is `"commonjs"`.

The package scope applies not only to initial entry points (`node my-app.js`)
but also to files referenced by `import` statements and `import()` expressions.

```js
// my-app.js, in an ES module package scope because there is a package.json
// file in the same folder with "type": "module".

import './startup/init.js';
// Loaded as ES module since ./startup contains no package.json file,
// and therefore inherits the ES module package scope from one level up.

import 'commonjs-package';
// Loaded as CommonJS since ./node_modules/commonjs-package/package.json
// lacks a "type" field or contains "type": "commonjs".

import './node_modules/commonjs-package/index.js';
// Loaded as CommonJS since ./node_modules/commonjs-package/package.json
// lacks a "type" field or contains "type": "commonjs".
```

Files ending with `.mjs` are always loaded as ES modules regardless of package
scope.

Files ending with `.cjs` are always loaded as CommonJS regardless of package
scope.

```js
import './legacy-file.cjs';
// Loaded as CommonJS since .cjs is always loaded as CommonJS.

import 'commonjs-package/src/index.mjs';
// Loaded as ES module since .mjs is always loaded as ES module.
```

The `.mjs` and `.cjs` extensions may be used to mix types within the same
package scope:

* Within a `"type": "module"` package scope, Node.js can be instructed to
  interpret a particular file as CommonJS by naming it with a `.cjs` extension
  (since both `.js` and `.mjs` files are treated as ES modules within a
  `"module"` package scope).

* Within a `"type": "commonjs"` package scope, Node.js can be instructed to
  interpret a particular file as an ES module by naming it with an `.mjs`
  extension (since both `.js` and `.cjs` files are treated as CommonJS within a
  `"commonjs"` package scope).

