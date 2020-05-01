<!-- YAML
added:
 - v12.0.0
 - v10.20.0
-->

* `value` {bigint} 要写入 `buf` 的数值。
* `offset` {integer} 开始写入之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 8`。**默认值:** `0`。
* 返回: {integer} `offset` 加上已写入的字节数。

用指定的[字节序][endianness]（`writeBigInt64BE()` 写入为大端序，`writeBigInt64LE()` 写入为小端序）将 `value` 写入到 `buf` 中指定的 `offset` 位置。

`value` 会被解析并写入为二进制补码的有符号整数。

```js
const buf = Buffer.allocUnsafe(8);

buf.writeBigInt64BE(0x0102030405060708n, 0);

console.log(buf);
// 打印: <Buffer 01 02 03 04 05 06 07 08>
```

