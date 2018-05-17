<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a number object, e.g. created
by `new Number()`.

For example:

```js
util.types.isNumberObject(0);  // Returns false
util.types.isNumberObject(new Number(0));   // Returns true
```

