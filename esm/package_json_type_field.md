
Files ending with `.js` will be loaded as ES modules when the nearest parent
`package.json` file contains a top-level field `"type"` with a value of
`"module"`.

The nearest parent `package.json` is defined as the first `package.json` found
when searching in the current folder, that folder’s parent, and so on up
until the root of the volume is reached.

<!-- eslint-skip -->
```js
// package.json
{
  "type": "module"
}
```

```bash
# In same folder as above package.json
node my-app.js # Runs as ES module
```

If the nearest parent `package.json` lacks a `"type"` field, or contains
`"type": "commonjs"`, `.js` files are treated as CommonJS. If the volume root is
reached and no `package.json` is found, Node.js defers to the default, a
`package.json` with no `"type"` field.

`import` statements of `.js` files are treated as ES modules if the nearest
parent `package.json` contains `"type": "module"`.

```js
// my-app.js, part of the same example as above
import './startup.js'; // Loaded as ES module because of package.json
```

Package authors should include the `"type"` field, even in packages where all
sources are CommonJS. Being explicit about the `type` of the package will
future-proof the package in case the default type of Node.js ever changes, and
it will also make things easier for build tools and loaders to determine how the
files in the package should be interpreted.

Regardless of the value of the `"type"` field, `.mjs` files are always treated
as ES modules and `.cjs` files are always treated as CommonJS.

