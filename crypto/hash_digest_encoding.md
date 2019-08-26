<!-- YAML
added: v0.1.92
-->
* `encoding` {string} 返回值的[字符编码][encoding]。
* 返回: {Buffer | string}


计算所有需要被哈希化的数据摘要 (通过 [`hash.update()`][] 方法)。 
如果提供了 `encoding` 则返回字符串，否则返回 [`Buffer`][]。

`Hash` 对象在 `hash.digest()` 方法调用之后不能再次被使用。多次的调用会引发错误并抛出。
