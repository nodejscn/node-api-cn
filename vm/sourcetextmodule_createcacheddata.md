<!-- YAML
added: v13.7.0
-->

* Returns: {Buffer}

Creates a code cache that can be used with the `SourceTextModule` constructor's
`cachedData` option. Returns a `Buffer`. This method may be called any number
of times before the module has been evaluated.

```js
// Create an initial module
const module = new vm.SourceTextModule('const a = 1;');

// Create cached data from this module
const cachedData = module.createCachedData();

// Create a new module using the cached data. The code must be the same.
const module2 = new vm.SourceTextModule('const a = 1;', { cachedData });
```

