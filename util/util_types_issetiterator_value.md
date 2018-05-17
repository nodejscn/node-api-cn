<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is an iterator returned for a built-in
[`Set`][] instance.

For example:

```js
const set = new Set();
util.types.isSetIterator(set.keys());  // Returns true
util.types.isSetIterator(set.values());  // Returns true
util.types.isSetIterator(set.entries());  // Returns true
util.types.isSetIterator(set[Symbol.iterator]());  // Returns true
```

