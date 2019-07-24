
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`string_decoder` 模块提供了一个 API，用于以保留编码的多字节 UTF-8 和 UTF-16 字符的方式将 `Buffer` 对象解码为字符串。
它可以使用以下方式访问：

```js
const { StringDecoder } = require('string_decoder');
```

以下示例展示了 `StringDecoder` 类的基本用法：

```js
const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent));

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro));
```

将 `Buffer` 实例写入 `StringDecoder` 实例时，将使用内部缓冲区来确保已解码的字符串不包含任何不完整的多字节字符。
它们保存在缓冲区中，直到下一次调用 `stringDecoder.write()` 或调用 `stringDecoder.end()` 为止。

在以下示例中，欧洲欧元符号（`€`）的三个 UTF-8 编码字节通过三次单独的操作写入：

```js
const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC])));
```

