<!-- YAML
added:
 - v12.0.0
 - v10.20.0
-->

* `offset` {integer} 开始读取之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 8`。**默认值:** `0`。
* 返回: {bigint}

用指定的[字节序][endianness]（`readBigInt64BE()` 读取为大端序，`readBigInt64LE()` 读取为小端序）从 `buf` 中指定的 `offset` 读取一个有符号的 64 位整数值。

从 `Buffer` 中读取的整数值会被解析为二进制补码值。

