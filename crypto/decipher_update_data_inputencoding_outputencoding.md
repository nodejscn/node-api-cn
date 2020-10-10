<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->

* `data` {string | Buffer | TypedArray | DataView}
* `inputEncoding` {string} 数据的[字符编码][encoding]。
* `outputEncoding` {string} 返回值的[字符编码][encoding]。
* 返回: {Buffer | string}

使用 `data` 更新解密。
如果指定了 `inputEncoding` 参数，则 `data` 参数是使用了指定的字符编码的字符串。
如果未指定 `inputEncoding` 参数，则 `data` 必须是一个 [`Buffer`]、`TypedArray` 或 `DataView`。
如果 `data` 是一个 [`Buffer`]、`TypedArray` 或 `DataView`，则 `inputEncoding` 会被忽略。

`outputEncoding` 指定了解密的数据的输出格式。
如果指定了 `outputEncoding`，则返回使用了指定的字符编码的字符串。
如果未提供 `outputEncoding`，则返回 [`Buffer`]。

可以使用新数据多次调用 `decipher.update()` 方法，直到 [`decipher.final()`] 被调用。 
在 [`decipher.final()`] 之后调用 `decipher.update()` 将会导致抛出错误。

