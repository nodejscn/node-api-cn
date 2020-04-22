<!-- YAML
added: v10.0.0
deprecated: v14.0.0
-->

> Stability: 0 - Deprecated: Use `value instanceof WebAssembly.Module` instead.

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`WebAssembly.Module`][] instance.

```js
const module = new WebAssembly.Module(wasmBuffer);
util.types.isWebAssemblyCompiledModule(module);  // Returns true
```

