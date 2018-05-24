<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a `BigUint64Array` instance. The
`--harmony-bigint` command line flag is required in order to use the
`BigUint64Array` type, but it is not required in order to use
`isBigUint64Array()`.

For example:

```js
util.types.isBigUint64Array(new BigInt64Array());   // Returns false
util.types.isBigUint64Array(new BigUint64Array());  // Returns true
```

