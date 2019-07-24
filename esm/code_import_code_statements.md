
An `import` statement can reference either ES module or CommonJS JavaScript.
Other file types such as JSON and Native modules are not supported. For those,
use [`module.createRequire()`][].

`import` statements are permitted only in ES modules. For similar functionality
in CommonJS, see [`import()`][].

The _specifier_ of an `import` statement (the string after the `from` keyword)
can either be an URL-style relative path like `'./file.mjs'` or a package name
like `'fs'`.

Like in CommonJS, files within packages can be accessed by appending a path to
the package name.

```js
import { sin, cos } from 'geometry/trigonometry-functions.mjs';
```

> Currently only the “default export” is supported for CommonJS files or
> packages:
>
> <!-- eslint-disable no-duplicate-imports -->
> ```js
> import packageMain from 'commonjs-package'; // Works
>
> import { method } from 'commonjs-package'; // Errors
> ```
>
> There are ongoing efforts to make the latter code possible.

