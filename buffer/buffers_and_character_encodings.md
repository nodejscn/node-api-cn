<!-- YAML
changes:
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7111
    description: Introduced `latin1` as an alias for `binary`.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2859
    description: Removed the deprecated `raw` and `raws` encodings.
-->

`Buffer` 实例一般用于表示编码字符的序列，比如 UTF-8 、 UCS2 、 Base64 、或十六进制编码的数据。
通过使用显式的字符编码，就可以在 `Buffer` 实例与普通的 JavaScript 字符串之间进行相互转换。

例子：

```js
const buf = Buffer.from('hello world', 'ascii');

// 输出 68656c6c6f20776f726c64
console.log(buf.toString('hex'));

// 输出 aGVsbG8gd29ybGQ=
console.log(buf.toString('base64'));
```

Node.js 目前支持的字符编码包括：

* `'ascii'` - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。

* `'utf8'` - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。

* `'utf16le'` - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。

* `'ucs2'` - `'utf16le'` 的别名。

* `'base64'` - Base64 编码。当从字符串创建 `Buffer` 时，按照 [RFC4648 第 5 章]的规定，这种编码也将正确地接受“URL 与文件名安全字母表”。

* `'latin1'` - 一种把 `Buffer` 编码成一字节编码的字符串的方式（由 IANA 定义在 [RFC1345] 第 63 页，用作 Latin-1 补充块与 C0/C1 控制码）。

* `'binary'` - `'latin1'` 的别名。

* `'hex'` - 将每个字节编码为两个十六进制字符。

**注意**：现代浏览器遵循 [WHATWG 编码标准] 将 'latin1' 和 ISO-8859-1 别名为 win-1252。
这意味着当进行例如 `http.get()` 这样的操作时，如果返回的字符编码是 WHATWG 规范列表中的，则有可能服务器真的返回 win-1252 编码的数据，此时使用 `'latin1'` 字符编码可能会错误地解码数据。

