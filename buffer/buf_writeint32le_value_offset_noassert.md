<!-- YAML
added: v0.5.5
-->

* `value` {integer} 要写入 `buf` 的数值
* `offset` {integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - 4`
* `noAssert` {boolean} 是否跳过 `value` 和 `offset` 检验？**默认:** `false`
* 返回: {integer} `offset` 加上写入的字节数

用指定的字节序格式（`writeInt32BE()` 写入大端序，`writeInt32LE()` 写入小端序）写入 `value` 到 `buf` 中指定的 `offset` 位置。
`value` 应当是一个有效的有符号的32位整数。
当 `value` 不是一个有符号的32位整数时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的最后一位字节，但后果是不确定的。

`value` 会被解析并写入为二进制补码值。

例子：

```js
const buf = Buffer.allocUnsafe(8);

buf.writeInt32BE(0x01020304, 0);
buf.writeInt32LE(0x05060708, 4);

// 输出: <Buffer 01 02 03 04 08 07 06 05>
console.log(buf);
```

