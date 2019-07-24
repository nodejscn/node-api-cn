
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
// Throws - Package exports error
```

> Note: this is not a strong encapsulation as any private modules can still be
> loaded by absolute paths.

Folders can also be mapped with package exports as well:

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
This is just a convention that works because `false`, just like `{}`, has no
iterable own properties.

