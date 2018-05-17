<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint32Array`][] instance.

For example:

```js
util.types.isUint32Array(new ArrayBuffer());  // Returns false
util.types.isUint32Array(new Uint32Array());  // Returns true
util.types.isUint32Array(new Float64Array());  // Returns false
```

