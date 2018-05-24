<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a `BigInt64Array` instance. The
`--harmony-bigint` command line flag is required in order to use the
`BigInt64Array` type, but it is not required in order to use
`isBigInt64Array()`.

For example:

```js
util.types.isBigInt64Array(new BigInt64Array());   // Returns true
util.types.isBigInt64Array(new BigUint64Array());  // Returns false
```

