<!-- YAML
added: v12.7.0
-->

When using the [`"exports"`][] field, custom subpaths can be defined along
with the main entry point by treating the main entry point as the
`"."` subpath:

```json
{
  "main": "./main.js",
  "exports": {
    ".": "./main.js",
    "./submodule": "./src/submodule.js"
  }
}
```

Now only the defined subpath in [`"exports"`][] can be imported by a consumer:

```js
import submodule from 'es-module-package/submodule';
// Loads ./node_modules/es-module-package/src/submodule.js
```

While other subpaths will error:

```js
import submodule from 'es-module-package/private-module.js';
// Throws ERR_PACKAGE_PATH_NOT_EXPORTED
```

