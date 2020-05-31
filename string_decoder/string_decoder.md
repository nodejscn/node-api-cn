
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`string_decoder` 模块提供了一个 API，用一种能保护已编码的多字节 UTF-8 和 UTF-16 字符的方式将 `Buffer` 对象解码为字符串。
可以使用以下方式访问它：

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

将 `Buffer` 实例写入 `StringDecoder` 实例时，会使用一个内部 buffer 来确保解码的字符串不包含任何不完整的多字节字符。
不完整的字符会被保存在该 buffer 中，直到下次调用 `stringDecoder.write()` 或调用 `stringDecoder.end()`。

在以下示例中，欧洲的欧元符号（`€`）的三个 UTF-8 编码字节通过三次单独的操作写入：

```js
const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC])));
```

