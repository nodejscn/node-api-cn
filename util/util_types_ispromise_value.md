<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a built-in [`Promise`][].

For example:

```js
util.types.isPromise(Promise.resolve(42));  // Returns true
```

