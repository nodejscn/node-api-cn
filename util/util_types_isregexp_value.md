<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a regular expression object.

For example:

```js
util.types.isRegExp(/abc/);  // Returns true
util.types.isRegExp(new RegExp('abc'));  // Returns true
```

