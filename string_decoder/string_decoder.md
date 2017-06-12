
> 稳定性: 2 - 稳定的

`string_decoder` 模块提供了一个 API，用于解码 `Buffer` 对象成字符串。它可以通过以下方式被使用：

```js
const { StringDecoder } = require('string_decoder');
```

以下例子展示了 `StringDecoder` 类的基本用法。

```js
const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent));

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro));
```

当一个 `Buffer` 实例被写入 `StringDecoder` 实例时，一个内部的 buffer 会被用于确保解码后的字符串不包含任何不完整的多字节字符。
不完整的多字节字符被保存在 buffer 中，直到下次调用 `stringDecoder.write()` 或直到 `stringDecoder.end()` 被调用。

以下例子中，欧元符号（`€`）的三个 UTF-8 编码的字节被分成三次操作写入：

```js
const { StringDecoder } = require('string_decoder');
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC])));
```

