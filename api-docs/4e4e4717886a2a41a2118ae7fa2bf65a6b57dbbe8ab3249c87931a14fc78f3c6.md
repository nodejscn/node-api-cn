<!-- YAML
added: v1.0.0
-->

当使用经验证的加密模式时(目前只有`GCM`支持),`cipher.getAuthTag()`方法返回一个[`Buffer`][]，此[`Buffer`][]包含已从给定数据计算后的_authentication tag_。
`cipher.getAuthTag()`方法只能在使用[`cipher.final()`][]方法完全加密后调用。


