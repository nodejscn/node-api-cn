<!-- YAML
added: v0.1.94
-->

* `encoding` {string} 返回值的[字符编码][encoding]。
* 返回: {Buffer | string}

计算使用 [`hmac.update()`] 传入的所有数据的 HMAC 摘要。 
如果提供了 `encoding`，则返回字符串，否则返回 [`Buffer`]。

调用 `hmac.digest()` 方法之后，`Hmac` 对象不能被再次使用。
多次调用 `hmac.digest()` 将会导致抛出错误。
