
The _specifier_ of an `import` statement is the string after the `from` keyword,
e.g. `'path'` in `import { sep } from 'path'`. Specifiers are also used in
`export from` statements, and as the argument to an `import()` expression.

There are four types of specifiers:

* _Bare specifiers_ like `'some-package'`. They refer to an entry point of a
  package by the package name.

* _Deep import specifiers_ like `'some-package/lib/shuffle.mjs'`. They refer to
  a path within a package prefixed by the package name.

* _Relative specifiers_ like `'./startup.js'` or `'../config.mjs'`. They refer
  to a path relative to the location of the importing file.

* _Absolute specifiers_ like `'file:///opt/nodejs/config.js'`. They refer
  directly and explicitly to a full path.

Bare specifiers, and the bare specifier portion of deep import specifiers, are
strings; but everything else in a specifier is a URL.

`file:`, `node:`, and `data:` URLs are supported. A specifier like
`'https://example.com/app.js'` may be supported by browsers but it is not
supported in Node.js.

Specifiers may not begin with `/` or `//`. These are reserved for potential
future use. The root of the current volume may be referenced via `file:///`.

