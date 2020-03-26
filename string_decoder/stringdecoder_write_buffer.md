<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: 现在，每个无效的字符（而不是每个字节）会被替换为一个替代字符。
-->

* `buffer` {Buffer|TypedArray|DataView} 包含要解码的字节的 `Buffer`、`TypedArray` 或 `DataView`。
* 返回: {string}

返回解码的字符串，会确保返回的字符串不会包含 `Buffer`、`TypedArray` 或 `DataView` 末尾中的任何不完整的多字节字符，并且会将不完整的字符保存在内部的 buffer 中用于下次调用 `stringDecoder.write()` 或 `stringDecoder.end()`。

