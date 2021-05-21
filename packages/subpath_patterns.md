<!-- YAML
added:
  - v14.13.0
  - v12.20.0
-->

For packages with a small number of exports or imports, we recommend
explicitly listing each exports subpath entry. But for packages that have
large numbers of subpaths, this might cause `package.json` bloat and
maintenance issues.

For these use cases, subpath export patterns can be used instead:

```json
// ./node_modules/es-module-package/package.json
{
  "exports": {
    "./features/*": "./src/features/*.js"
  },
  "imports": {
    "#internal/*": "./src/internal/*.js"
  }
}
```

The left hand matching pattern must always end in `*`. All instances of `*` on
the right hand side will then be replaced with this value, including if it
contains any `/` separators.

```js
import featureX from 'es-module-package/features/x';
// Loads ./node_modules/es-module-package/src/features/x.js

import featureY from 'es-module-package/features/y/y';
// Loads ./node_modules/es-module-package/src/features/y/y.js

import internalZ from '#internal/z';
// Loads ./node_modules/es-module-package/src/internal/z.js
```

This is a direct static replacement without any special handling for file
extensions. In the previous example, `pkg/features/x.json` would be resolved to
`./src/features/x.json.js` in the mapping.

The property of exports being statically enumerable is maintained with exports
patterns since the individual exports for a package can be determined by
treating the right hand side target pattern as a `**` glob against the list of
files within the package. Because `node_modules` paths are forbidden in exports
targets, this expansion is dependent on only the files of the package itself.

