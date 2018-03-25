<!-- YAML
added: v1.0.0
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9398
    description: This method now returns a reference to `decipher`.
-->
- `buffer` {Buffer | TypedArray | DataView}
- 返回{cipher}的一个方法链。

当使用经过验证的加密模式（当前仅支持`GCM`）时，`decipher.setAAD()`方法会设置用于附加验证数据(AAD)输入参数的值。

`decipher.setAAD()` 必须在[`decipher.update()`][]之前被调用。
