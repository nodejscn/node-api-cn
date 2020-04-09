
An `import` statement can reference an ES module or a CommonJS module. Other
file types such as JSON or Native modules are not supported. For those, use
[`module.createRequire()`][].

`import` statements are permitted only in ES modules. For similar functionality
in CommonJS, see [`import()`][].

The _specifier_ of an `import` statement (the string after the `from` keyword)
can either be an URL-style relative path like `'./file.mjs'` or a package name
like `'fs'`.

Like in CommonJS, files within packages can be accessed by appending a path to
the package name; unless the package’s `package.json` contains an `"exports"`
field, in which case files within packages need to be accessed via the path
defined in `"exports"`.

```js
import { sin, cos } from 'geometry/trigonometry-functions.mjs';
```

Only the “default export” is supported for CommonJS files or packages:

<!-- eslint-disable no-duplicate-imports -->
```js
import packageMain from 'commonjs-package'; // Works

import { method } from 'commonjs-package'; // Errors
```

It is also possible to
[import an ES or CommonJS module for its side effects only][].

