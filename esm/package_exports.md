
By default, all subpaths from a package can be imported (`import 'pkg/x.js'`).
Custom subpath aliasing and encapsulation can be provided through the
`"exports"` field.

<!-- eslint-skip -->
```js
// ./node_modules/es-module-package/package.json
{
  "exports": {
    "./submodule": "./src/submodule.js"
  }
}
```

```js
import submodule from 'es-module-package/submodule';
// Loads ./node_modules/es-module-package/src/submodule.js
```

In addition to defining an alias, subpaths not defined by `"exports"` will
throw when an attempt is made to import them:

```js
import submodule from 'es-module-package/private-module.js';
// Throws ERR_MODULE_NOT_FOUND
```

> Note: this is not a strong encapsulation as any private modules can still be
> loaded by absolute paths.

Folders can also be mapped with package exports:

<!-- eslint-skip -->
```js
// ./node_modules/es-module-package/package.json
{
  "exports": {
    "./features/": "./src/features/"
  }
}
```

```js
import feature from 'es-module-package/features/x.js';
// Loads ./node_modules/es-module-package/src/features/x.js
```

If a package has no exports, setting `"exports": false` can be used instead of
`"exports": {}` to indicate the package does not intend for submodules to be
exposed.

Any invalid exports entries will be ignored. This includes exports not
starting with `"./"` or a missing trailing `"/"` for directory exports.

Array fallback support is provided for exports, similarly to import maps
in order to be forwards-compatible with possible fallback workflows in future:

<!-- eslint-skip -->
```js
{
  "exports": {
    "./submodule": ["not:valid", "./submodule.js"]
  }
}
```

Since `"not:valid"` is not a supported target, `"./submodule.js"` is used
instead as the fallback, as if it were the only target.

Defining a `"."` export will define the main entry point for the package,
and will always take precedence over the `"main"` field in the `package.json`.

This allows defining a different entry point for Node.js versions that support
ECMAScript modules and versions that don't, for example:

<!-- eslint-skip -->
```js
{
  "main": "./main-legacy.cjs",
  "exports": {
    ".": "./main-modern.cjs"
  }
}
```

