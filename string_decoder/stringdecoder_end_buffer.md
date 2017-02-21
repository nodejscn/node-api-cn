<!-- YAML
added: v0.9.3
-->

* `buffer` {Buffer} 一个包含了要解码的字节的 `Buffer`。

以字符串的形式返回任何剩下的被保存在内部 buffer 中的字节。
不完整的 UTF-8 与 UTF-16 字符的字节会被替换成符合字符编码的替代字符。

如果提供了 `buffer` 参数，则在返回剩余字节之前会再执行一次 `stringDecoder.write()`。

