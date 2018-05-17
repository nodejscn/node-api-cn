<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`DataView`][] instance.

For example:

```js
const ab = new ArrayBuffer(20);
util.types.isDataView(new DataView(ab));  // Returns true
util.types.isDataView(new Float64Array());  // Returns false
```

See also [`ArrayBuffer.isView()`][].

