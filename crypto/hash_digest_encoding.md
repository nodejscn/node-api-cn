<!-- YAML
added: v0.1.92
-->
- `encoding` {string}
- Returns: {Buffer | string}


计算所有需要被哈希化的数据摘要 (通过
[`hash.update()`][] 方法)。 `encoding` 值可以是 `'hex'`, `'latin1'` 或者
`'base64'`. 如果`encoding` 春如的是字符串会被直接返回; 其它情况会返回一个
a [`Buffer`][].

`Hash` 对象在 `hash.digest()` 方法调用之后不能再次被使用。多次的调用会引发错误并抛出。
