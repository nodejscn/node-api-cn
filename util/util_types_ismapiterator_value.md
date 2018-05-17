<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is an iterator returned for a built-in
[`Map`][] instance.

For example:

```js
const map = new Map();
util.types.isMapIterator(map.keys());  // Returns true
util.types.isMapIterator(map.values());  // Returns true
util.types.isMapIterator(map.entries());  // Returns true
util.types.isMapIterator(map[Symbol.iterator]());  // Returns true
```

