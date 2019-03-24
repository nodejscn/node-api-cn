<!-- YAML
added: v10.0.0
-->

* `value` {any}
* Returns: {boolean}

Returns `true` if the value is a number object, e.g. created
by `new Number()`.

```js
util.types.isNumberObject(0);  // Returns false
util.types.isNumberObject(new Number(0));   // Returns true
```

