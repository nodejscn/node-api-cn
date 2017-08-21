<!-- YAML
added: v0.9.3
-->

* `buffer` {Buffer} 包含待解码字节的 `Buffer`。

以字符串的形式返回内部 buffer 中剩余的字节。
残缺的 UTF-8 与 UTF-16 字符的字节会被替换成符合字符编码的字符。

如果提供了 `buffer` 参数，则在返回剩余字节之前会再执行一次 `stringDecoder.write()`。

