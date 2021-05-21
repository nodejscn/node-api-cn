
> Stability: 1 - Experimental

This feature is only available with the `--experimental-import-meta-resolve`
command flag enabled.

* `specifier` {string} The module specifier to resolve relative to `parent`.
* `parent` {string|URL} The absolute parent module URL to resolve from. If none
  is specified, the value of `import.meta.url` is used as the default.
* Returns: {Promise}

Provides a module-relative resolution function scoped to each module, returning
the URL string.

<!-- eslint-skip -->
```js
const dependencyAsset = await import.meta.resolve('component-lib/asset.css');
```

`import.meta.resolve` also accepts a second argument which is the parent module
from which to resolve from:

<!-- eslint-skip -->
```js
await import.meta.resolve('./dep', import.meta.url);
```

This function is asynchronous because the ES module resolver in Node.js is
allowed to be asynchronous.

