<!-- YAML
added: v0.9.3
-->

* `buffer` {Buffer|TypedArray|DataView} 包含要解码的字节的 `Buffer`、`TypedArray` 或 `DataView`。
* 返回: {string}

以字符串形式返回存储在内部缓冲区中的任何剩余输入。 
表示不完整的 UTF-8 和 UTF-16 字符的字节将替换为适合字符编码的替换字符。

如果提供了 `buffer` 参数，则在返回剩余的输入之前再最后一次调用 `stringDecoder.write()`。

