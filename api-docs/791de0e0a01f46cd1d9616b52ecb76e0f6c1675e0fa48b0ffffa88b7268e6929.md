<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a built-in [`Promise`][].

```js
util.types.isPromise(Promise.resolve(42));  // Returns true
```

