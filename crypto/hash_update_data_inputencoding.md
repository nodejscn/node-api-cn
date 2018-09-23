<!-- YAML
added: v0.1.92
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}

Updates the hash content with the given `data`, the encoding of which
is given in `inputEncoding` and can be `'utf8'`, `'ascii'` or
`'latin1'`. If `encoding` is not provided, and the `data` is a string, an
encoding of `'utf8'` is enforced. If `data` is a [`Buffer`][], `TypedArray`, or
`DataView`, then `inputEncoding` is ignored.

This can be called many times with new data as it is streamed.

<!-- YAML
新增于: v0.1.92
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}

根据 `data`更新hash的内容,编码方式为 `inputEncoding`可以是 `'utf8'`, `'ascii'` 或者
`'latin1'`. 如果 `encoding` 没有传值, `data` 是一个字符串, 强制编码格式为`'utf8'`。
如果 `data` 是 [`Buffer`][], `TypedArray`, 或者
`DataView`,  `inputEncoding` 会被忽略.

因为流的特点这个方法可以通过新的值被多次调用。
