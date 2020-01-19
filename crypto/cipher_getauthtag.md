<!-- YAML
added: v1.0.0
-->

* 返回: {Buffer} 当使用经验证的加密模式时（目前只支持 `GCM`、`CCM` 和 `OCB`），`cipher.getAuthTag()` 方法返回一个 [`Buffer`][]，它包含已从给定数据计算后的认证标签。

`cipher.getAuthTag()` 方法只能在使用 [`cipher.final()`][] 方法完全加密后调用。


