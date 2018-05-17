<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is an `arguments` object.

For example:

<!-- eslint-disable prefer-rest-params -->
```js
function foo() {
  util.types.isArgumentsObject(arguments);  // Returns true
}
```

