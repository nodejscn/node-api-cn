
To set the main entry point for a package, it is advisable to define both
[`"exports"`][] and [`"main"`][] in the package’s [`package.json`][] file:

```json
{
  "main": "./main.js",
  "exports": "./main.js"
}
```

When the [`"exports"`][] field is defined, all subpaths of the package are
encapsulated and no longer available to importers. For example,
`require('pkg/subpath.js')` throws an [`ERR_PACKAGE_PATH_NOT_EXPORTED`][]
error.

This encapsulation of exports provides more reliable guarantees
about package interfaces for tools and when handling semver upgrades for a
package. It is not a strong encapsulation since a direct require of any
absolute subpath of the package such as
`require('/path/to/node_modules/pkg/subpath.js')` will still load `subpath.js`.

