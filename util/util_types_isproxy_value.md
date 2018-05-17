<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a [`Proxy`][] instance.

For example:

```js
const target = {};
const proxy = new Proxy(target, {});
util.types.isProxy(target);  // Returns false
util.types.isProxy(proxy);  // Returns true
```

