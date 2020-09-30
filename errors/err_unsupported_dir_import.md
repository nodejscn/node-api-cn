
`import` a directory URL is unsupported. Instead,
[self-reference a package using its name][] and [define a custom subpath][] in
the [`"exports"`][] field of the [`package.json`][] file.

<!-- eslint-skip -->
```js
import './'; // unsupported
import './index.js'; // supported
import 'package-name'; // supported
```

<a id="ERR_UNSUPPORTED_ESM_URL_SCHEME"></a>
