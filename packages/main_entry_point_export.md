
To set the main entry point for a package, it is advisable to define both
[`"exports"`][] and [`"main"`][] in the package’s [`package.json`][] file:

```json
{
  "main": "./main.js",
  "exports": "./main.js"
}
```

When defining the [`"exports"`][] field, all subpaths of the package will be
encapsulated and no longer available to importers. For example,
`require('pkg/subpath.js')` would throw an [`ERR_PACKAGE_PATH_NOT_EXPORTED`][]
error.

This encapsulation of exports provides more reliable guarantees
about package interfaces for tools and when handling semver upgrades for a
package. It is not a strong encapsulation since a direct require of any
absolute subpath of the package such as
`require('/path/to/node_modules/pkg/subpath.js')` will still load `subpath.js`.

