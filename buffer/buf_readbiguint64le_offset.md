<!-- YAML
added:
 - v12.0.0
 - v10.20.0
-->

* `offset` {integer} 开始读取之前要跳过的字节数。必须满足：`0 <= offset <= buf.length - 8`。**默认值:** `0`。
* 返回: {bigint}

用指定的[字节序][endianness]（`readBigUInt64BE()` 读取为大端序，`readBigUInt64LE()` 读取为小端序）从 `buf` 中指定的 `offset` 读取一个无符号的 64 位整数值。

```js
const buf = Buffer.from([0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff]);

console.log(buf.readBigUInt64BE(0));
// 打印: 4294967295n

console.log(buf.readBigUInt64LE(0));
// 打印: 18446744069414584320n
```

