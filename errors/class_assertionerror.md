
`Error` 的子类，表示断言失败。 这种错误通常表示实际值和预期值不相等。

比如:

```js
assert.strictEqual(1, 2);
// AssertionError [ERR_ASSERTION]: 1 === 2
```

