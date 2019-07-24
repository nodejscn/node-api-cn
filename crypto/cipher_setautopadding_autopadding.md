<!-- YAML
added: v0.7.1
-->
- `autoPadding` {boolean} 默认为 `true`.
- 返回{Cipher}方法链。

当使用块加密算法时，`Cipher`类会自动添加padding到输入数据中，来适配相应块大小。可调用`cipher.setAutoPadding(false)`禁用默认padding。

当`autoPadding`是`false`时，整个输入数据的长度必须是cipher块大小的倍数，否则[`cipher.final()`][]将抛出一个错误。
禁用自动填充对于非标准填充是有用的，例如使用`0x0`代替PKCS填充。

`cipher.setAutoPadding()`必须在[`cipher.final()`][]之前被调用。

