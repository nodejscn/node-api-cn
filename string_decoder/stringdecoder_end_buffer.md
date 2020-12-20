<!-- YAML
added: v0.9.3
-->

* `buffer` {Buffer|TypedArray|DataView} 包含要解码的字节的 `Buffer`、`TypedArray` 或 `DataView`。
* 返回: {string}

以字符串的形式返回保存在内部 buffer 中的所有的剩余的输入。 
不完整的 UTF-8 和 UTF-16 字符的字节将会被替换为适合字符编码的替代字符。

如果提供了 `buffer` 参数，则在返回剩余的输入之前会再最后一次调用 `stringDecoder.write()`。
调用完 `end()` 之后，`stringDecoder` 对象可被重新用于新的输入。

