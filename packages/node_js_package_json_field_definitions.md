
This section describes the fields used by the Node.js runtime. Other tools (such
as [npm](https://docs.npmjs.com/creating-a-package-json-file)) use
additional fields which are ignored by Node.js and not documented here.

The following fields in `package.json` files are used in Node.js:

* [`"name"`][] - Relevant when using named imports within a package. Also used
  by package managers as the name of the package.
* [`"type"`][] - The package type determining whether to load `.js` files as
  CommonJS or ES modules.
* [`"exports"`][] - Package exports and conditional exports. When present,
  limits which submodules can be loaded from within the package.
* [`"main"`][] - The default module when loading the package, if exports is not
  specified, and in versions of Node.js prior to the introduction of exports.
* [`"imports"`][] - Package imports, for use by modules within the package
  itself.

