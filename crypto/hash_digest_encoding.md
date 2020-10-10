<!-- YAML
added: v0.1.92
-->

* `encoding` {string} 返回值的[字符编码][encoding]。
* 返回: {Buffer | string}


计算传入要被哈希（使用 [`hash.update()`] 方法）的所有数据的摘要。 
如果提供了 `encoding`，则返回字符串，否则返回 [`Buffer`]。

调用 `hash.digest()` 方法之后，`Hash` 对象不能被再次使用。
多次调用将会导致抛出错误。

