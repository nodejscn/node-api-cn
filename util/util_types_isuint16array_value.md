<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`Uint16Array`][] instance.

For example:

```js
util.types.isUint16Array(new ArrayBuffer());  // Returns false
util.types.isUint16Array(new Uint16Array());  // Returns true
util.types.isUint16Array(new Float64Array());  // Returns false
```

