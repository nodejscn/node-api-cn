<!-- YAML
added: v0.1.92
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
