<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}
- `outputEncoding` {string}

使用新数据更新解密。如果给出`inputEncoding`参数，它的值必须是`'latin1'`, `'base64'`或`'hex'`中的一个，`data`参数是使用指定编码的字符串。如果未给出`inputEncoding`参数，则`data`必须是[`Buffer`][]。如果`data`是[`Buffer`][]，则忽略`inputEncoding`。

`outputEncoding`指定加密数据的输出格式，可以是`'latin1'`, `'ascii'`或`'utf8'`。如果指定了`outputEncoding`，则返回使用指定编码的字符串。如果未提供`outputEncoding`，则返回[`Buffer`][]。

可以使用新数据多次调用`decipher.update()`方法，直到调用[`decipher.final()`][]。在[`decipher.final()`][]之后调用`decipher.update()`会导致抛出错误。
