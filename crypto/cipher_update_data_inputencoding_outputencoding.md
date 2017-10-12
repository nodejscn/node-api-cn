<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: 默认`inputEncoding`由`binary` 变为 `utf8`
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}
- `outputEncoding` {string}

用`data`更新密码。如果给出了`inputEncoding`的论证，它的值必须是`'utf8'`, `'ascii'`, 或者`'latin1'`，而`data`参数是使用指定编码的字符串。如果不给出`inputEncoding`的参数，则`data`必须是[`Buffer`][]，`TypedArray`， 或者`DataView`。如果`data`是一个[`Buffer`][]，`TypedArray`， 或者 `DataView`， 那么`inputEncoding`就被忽略了。

`outputEncoding`指定了加密数据的输出格式，可以是`'latin1'`， `'base64'` 或者 `'hex'`。如果指定了`outputEncoding`，则返回使用指定编码的字符串。如果没有`outputEncoding`被提供，会返回[`Buffer`][]。

`cipher.update()`方法可以用新数据多次调用，直到[`cipher.final()`][]被调用。
[' cipher.final()'][]。在[`cipher.final()`][]之后调用`cipher.update()`将抛出错误。

