<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`WebAssembly.Module`][] instance.

For example:

```js
const module = new WebAssembly.Module(wasmBuffer);
util.types.isWebAssemblyCompiledModule(module);  // Returns true
```

