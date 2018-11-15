<!-- YAML
changes:
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7111
    description: Introduced `latin1` as an alias for `binary`.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2859
    description: Removed the deprecated `raw` and `raws` encodings.
-->

当 `Buffer` 存入或取出字符串时，需要指定字符编码。

例子：

```js
const buf = Buffer.from('hello world', 'ascii');

console.log(buf.toString('hex'));
// 输出: 68656c6c6f20776f726c64

console.log(buf.toString('base64'));
// 输出: aGVsbG8gd29ybGQ=

console.log(Buffer.from('fhqwhgads', 'ascii'));
// 输出: <Buffer 66 68 71 77 68 67 61 64 73>
console.log(Buffer.from('fhqwhgads', 'utf16le'));
// 输出: <Buffer 66 00 68 00 71 00 77 00 68 00 67 00 61 00 64 00 73 00>
```

Node.js 支持的字符编码有：

* `'ascii'` - 仅支持 7 位 ASCII 数据。

* `'utf8'` - 多字节编码的 Unicode 字符。

* `'utf16le'` - 2 或 4 个字节，小端序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。

* `'ucs2'` - `'utf16le'` 的别名。

* `'base64'` - Base64 编码。

* `'latin1'` - 将 `Buffer` 编码成单字节编码的字符串。

* `'binary'` - `'latin1'` 的别名。

* `'hex'` - 将每个字节编码成两个十六进制字符。

