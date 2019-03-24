<!-- YAML
added: v10.6.0
-->

* Returns: {Buffer}

Creates a code cache that can be used with the Script constructor's
`cachedData` option. Returns a Buffer. This method may be called at any
time and any number of times.

```js
const script = new vm.Script(`
function add(a, b) {
  return a + b;
}

const x = add(1, 2);
`);

const cacheWithoutX = script.createCachedData();

script.runInThisContext();

const cacheWithX = script.createCachedData();
```

