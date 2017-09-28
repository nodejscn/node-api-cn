<!-- YAML
added: v1.0.0
-->
- `buffer` {Buffer}
- 返回{Cipher}方法链。

当使用经过验证的加密模式(目前只支持`GCM`)时，`cipher.setAAD()`方法设置用于_additional authenticated data_(_附加验证的data_(AAD))输入参数的值。

`cipher.setAAD()`法必须在[`cipher.update()`][]之前调用。


