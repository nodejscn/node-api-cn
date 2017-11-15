<!-- YAML
added: v0.1.94
-->
- `outputEncoding` {string}

返回任何加密的内容。如果 `outputEncoding` 参数是`'latin1'`, `'base64'` 或者 `'hex'`，返回字符串。
如果没有提供 `outputEncoding`，则返回[`Buffer`][]。

一旦`cipher.final()`方法已被调用，`Cipher` 对象就不能再用于加密数据。如果试图再次调用`cipher.final()`，将会抛出一个错误。

