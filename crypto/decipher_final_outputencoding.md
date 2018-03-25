<!-- YAML
added: v0.1.94
-->
- `outputEncoding` {string}

返回任何剩余的解密内容。如果`outputEncoding`参数是'latin1'，'ascii'或'utf8'之一，则返回一个字符串。
如果未提供输出编码，则返回`Buffer`。

一旦调用了`decipher.final()`方法，`Decipher`对象就不能再用于解密数据。
试图不止一次调用`decipher.final()`会导致错误被抛出。
