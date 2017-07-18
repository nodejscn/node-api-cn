<!-- YAML
added: v0.5.8
-->

创建并返回一个带有给定 [options][] 的新的 [DeflateRaw][] 对象.

*注意*: zlib 库拒绝 256-字节的 windows 的请求 (即 `{windowBits: 8}` in `options`).
当创建具有这个特定 `windowBits` 值的 [DeflateRaw][] 对象时, 会抛出一个 `Error`
