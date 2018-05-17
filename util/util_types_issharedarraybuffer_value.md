<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`SharedArrayBuffer`][] instance.
This does *not* include [`ArrayBuffer`][] instances. Usually, it is
desirable to test for both; See [`util.types.isAnyArrayBuffer()`][] for that.

For example:

```js
util.types.isSharedArrayBuffer(new ArrayBuffer());  // Returns false
util.types.isSharedArrayBuffer(new SharedArrayBuffer());  // Returns true
```

