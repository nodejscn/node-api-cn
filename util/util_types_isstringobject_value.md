<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a string object, e.g. created
by `new String()`.

For example:

```js
util.types.isStringObject('foo');  // Returns false
util.types.isStringObject(new String('foo'));   // Returns true
```

