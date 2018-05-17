<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a symbol object, created
by calling `Object()` on a `Symbol` primitive.

For example:

```js
const symbol = Symbol('foo');
util.types.isSymbolObject(symbol);  // Returns false
util.types.isSymbolObject(Object(symbol));   // Returns true
```

