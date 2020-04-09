
To set the main entry point for a package, it is advisable to define both
`"exports"` and `"main"` in the package’s `package.json` file:

<!-- eslint-skip -->
```js
{
  "main": "./main.js",
  "exports": "./main.js"
}
```

The benefit of doing this is that when using the `"exports"` field all
subpaths of the package will no longer be available to importers under
`require('pkg/subpath.js')`, and instead they will get a new error,
`ERR_PACKAGE_PATH_NOT_EXPORTED`.

This encapsulation of exports provides more reliable guarantees
about package interfaces for tools and when handling semver upgrades for a
package. It is not a strong encapsulation since a direct require of any
absolute subpath of the package such as
`require('/path/to/node_modules/pkg/subpath.js')` will still load `subpath.js`.

