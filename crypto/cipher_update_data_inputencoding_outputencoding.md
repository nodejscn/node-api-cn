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

用 `data` 更新密码。
如果给定了 `inputEncoding`，则 `data` 参数是使用指定编码的字符串。
如果不给出 `inputEncoding` 的参数，则 `data` 必须是 [`Buffer`]、`TypedArray` 或者 `DataView`。
如果 `data` 是一个 [`Buffer`][]、`TypedArray` 或者 `DataView`，则 `inputEncoding` 会被忽略。

`outputEncoding` 指定了加密数据的输出格式。
如果指定了 `outputEncoding`，则返回使用指定编码的字符串。
如果没有 `outputEncoding` 被提供，则返回 [`Buffer`][]。

`cipher.update()` 方法可以用新数据多次调用，直到 [`cipher.final()`][] 被调用。
在 [`cipher.final()`][] 之后调用 `cipher.update()` 将抛出错误。

