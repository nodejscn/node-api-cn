<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`ArrayBuffer`][] instance.
This does *not* include [`SharedArrayBuffer`][] instances. Usually, it is
desirable to test for both; See [`util.types.isAnyArrayBuffer()`][] for that.

For example:

```js
util.types.isArrayBuffer(new ArrayBuffer());  // Returns true
util.types.isArrayBuffer(new SharedArrayBuffer());  // Returns false
```

