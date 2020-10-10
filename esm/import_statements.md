
An `import` statement can reference an ES module or a CommonJS module.
`import` statements are permitted only in ES modules. For similar functionality
in CommonJS, see [`import()`][].

When importing [CommonJS modules](#esm_commonjs_namespaces), the
`module.exports` object is provided as the default export. Named exports may be
available, provided by static analysis as a convenience for better ecosystem
compatibility.

Additional experimental flags are available for importing
[Wasm modules](#esm_experimental_wasm_modules) or
[JSON modules](#esm_experimental_json_modules). For importing native modules or
JSON modules unflagged, see [`module.createRequire()`][].

The _specifier_ of an `import` statement (the string after the `from` keyword)
can either be an URL-style relative path like `'./file.mjs'` or a package name
like `'fs'`.

Like in CommonJS, files within packages can be accessed by appending a path to
the package name; unless the package’s [`package.json`][] contains an
[`"exports"`][] field, in which case files within packages need to be accessed
via the path defined in [`"exports"`][].

```js
import { sin, cos } from 'geometry/trigonometry-functions.mjs';
```

