<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is an instance of a built-in [`Error`][] type.

For example:

```js
util.types.isNativeError(new Error());  // Returns true
util.types.isNativeError(new TypeError());  // Returns true
util.types.isNativeError(new RangeError());  // Returns true
```

