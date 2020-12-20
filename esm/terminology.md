
The _specifier_ of an `import` statement is the string after the `from` keyword,
e.g. `'path'` in `import { sep } from 'path'`. Specifiers are also used in
`export from` statements, and as the argument to an `import()` expression.

There are three types of specifiers:

* _Relative specifiers_ like `'./startup.js'` or `'../config.mjs'`. They refer
  to a path relative to the location of the importing file. _The file extension
  is always necessary for these._

* _Bare specifiers_ like `'some-package'` or `'some-package/shuffle'`. They can
  refer to the main entry point of a package by the package name, or a
  specific feature module within a package prefixed by the package name as per
  the examples respectively. _Including the file extension is only necessary
  for packages without an [`"exports"`][] field._

* _Absolute specifiers_ like `'file:///opt/nodejs/config.js'`. They refer
  directly and explicitly to a full path.

Bare specifier resolutions are handled by the [Node.js module resolution
algorithm][]. All other specifier resolutions are always only resolved with
the standard relative [URL][] resolution semantics.

Like in CommonJS, module files within packages can be accessed by appending a
path to the package name unless the package’s [`package.json`][] contains an
[`"exports"`][] field, in which case files within packages can only be accessed
via the paths defined in [`"exports"`][].

For details on these package resolution rules that apply to bare specifiers in
the Node.js module resolution, see the [packages documentation](packages.md).

