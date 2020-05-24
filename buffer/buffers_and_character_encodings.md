<!-- YAML
changes:
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7111
    description: Introduced `latin1` as an alias for `binary`.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2859
    description: Removed the deprecated `raw` and `raws` encodings.
-->

当在 `Buffer` 和字符串之间转换时，可以指定字符编码。 
如果未指定字符编码，则使用 UTF-8 作为默认值。

```js
const buf = Buffer.from('hello world', 'utf8');

console.log(buf.toString('hex'));
// 打印: 68656c6c6f20776f726c64
console.log(buf.toString('base64'));
// 打印: aGVsbG8gd29ybGQ=

console.log(Buffer.from('fhqwhgads', 'utf8'));
// 打印: <Buffer 66 68 71 77 68 67 61 64 73>
console.log(Buffer.from('fhqwhgads', 'utf16le'));
// 打印: <Buffer 66 00 68 00 71 00 77 00 68 00 67 00 61 00 64 00 73 00>
```

Node.js 当前支持的字符编码如下：

* `'utf8'`: 多字节编码的 Unicode 字符。
  许多网页和其他文档格式都使用 UTF-8。
  这是默认的字符编码。 
  当将 `Buffer` 解码为不专门包含有效 UTF-8 数据的字符串时，则会使用 Unicode 替换字符 `U+FFFD` � 来表示这些错误。

* `'utf16le'`: 多字节编码的 Unicode 字符。 
  与 `'utf8'` 不同，字符串中的每个字符都会使用 2 个或 4 个字节进行编码。 
  Node.js 仅支持 [UTF-16] 的[小端序][endianness]变体。

* `'latin1'`: Latin-1 代表 [ISO-8859-1]。 
  此字符编码仅支持从 `U+0000` 到 `U+00FF` 的 Unicode 字符。 
  每个字符使用单个字节进行编码。 
  超出该范围的字符会被截断，并映射成该范围内的字符。

使用以上方法之一将 `Buffer` 转换为字符串，称为解码；将字符串转换为 `Buffer`，称为编码。

Node.js 还支持以下两种二进制转文本的编码。 
对于二进制转文本的编码，其命名约定是相反的：将 `Buffer` 转换为字符串通常称为编码，而将字符串转换为 `Buffer` 则称为解码。

* `'base64'`: [Base64] 编码。
  当从字符串创建 `Buffer` 时，此编码也会正确地接受 [RFC 4648 第 5 节][RFC 4648, Section 5]中指定的 “URL 和文件名安全字母”。

* `'hex'`: 将每个字节编码成两个十六进制的字符。
  当解码仅包含有效的十六进制字符的字符串时，可能会发生数据截断。 
  请参见下面的示例。

还支持以下传统的字符编码：

* `'ascii'`: 仅适用于 7 位 [ASCII] 数据。
  当将字符串编码为 `Buffer` 时，这等效于使用 `'latin1'`。 
  当将 `Buffer` 解码为字符串时，则使用编码会在解码为 `'latin1'` 之前额外取消设置每个字节的最高位。 
  通常，当在编码或解码纯 ASCII 文本时，应该没有理由使用这种编码，因为 `'utf8'`（或者，如果已知的数据始终为纯 ASCII，则为 `'latin1'`）会是更好的选择。 
  这仅为传统的兼容性而提供。

* `'binary'`: `'latin1'` 的别名。
  有关此编码的更多背景，请参阅[二进制字符串][binary strings]。 
  该编码的名称可能会引起误解，因为此处列出的所有编码都是在字符串和二进制数据之间转换。 
  对于在字符串和 `Buffer` 之间进行转换，通常 `'utf-8'` 是正确的选择。

* `'ucs2'`: `'utf16le'` 的别名。
  UCS-2 以前是指 UTF-16 的一种变体，该变体不支持代码点大于 U+FFFF 的字符。 
  在 Node.js 中，始终支持这些代码点。

```js
Buffer.from('1ag', 'hex');
// 打印 <Buffer 1a>，当遇到第一个非十六进制的值（'g'）时，则数据会被截断。

Buffer.from('1a7g', 'hex');
// 打印 <Buffer 1a>，当数据以一个数字（'7'）结尾时，则数据会被截断。

Buffer.from('1634', 'hex');
// 打印 <Buffer 16 34>，所有数据均可用。
```

现代的 Web 浏览器遵循 [WHATWG 编码标准][WHATWG Encoding Standard]，将 `'latin1'` 和 `'ISO-8859-1'` 别名为 `'win-1252'`。
这意味着当执行 `http.get()` 之类的操作时，如果返回的字符集是 WHATWG 规范中列出的字符集之一，则服务器可能实际返回 `'win-1252'` 编码的数据，而使用 `'latin1'` 编码可能错误地解码字符。

