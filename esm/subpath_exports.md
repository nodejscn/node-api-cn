
When using the `"exports"` field, custom subpaths can be defined along
with the main entry point by treating the main entry point as the
`"."` subpath:

<!-- eslint-skip -->
```js
{
  "main": "./main.js",
  "exports": {
    ".": "./main.js",
    "./submodule": "./src/submodule.js"
  }
}
```

Now only the defined subpath in `"exports"` can be imported by a
consumer:

```js
import submodule from 'es-module-package/submodule';
// Loads ./node_modules/es-module-package/src/submodule.js
```

While other subpaths will error:

```js
import submodule from 'es-module-package/private-module.js';
// Throws ERR_PACKAGE_PATH_NOT_EXPORTED
```

Entire folders can also be mapped with package exports:

<!-- eslint-skip -->
```js
// ./node_modules/es-module-package/package.json
{
  "exports": {
    "./features/": "./src/features/"
  }
}
```

With the above, all modules within the `./src/features/` folder
are exposed deeply to `import` and `require`:

```js
import feature from 'es-module-package/features/x.js';
// Loads ./node_modules/es-module-package/src/features/x.js
```

When using folder mappings, ensure that you do want to expose every
module inside the subfolder. Any modules which are not public
should be moved to another folder to retain the encapsulation
benefits of exports.

