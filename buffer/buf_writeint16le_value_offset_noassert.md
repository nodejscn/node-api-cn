<!-- YAML
added: v0.5.5
-->

* `value` {integer} 要写入 `buf` 的数值
* `offset` {integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - 2`
* `noAssert` {boolean} 是否跳过 `value` 和 `offset` 检验？**默认:** `false`
* 返回: {integer} `offset` 加上写入的字节数

用指定的字节序格式（`writeInt16BE()` 写入大端序，`writeInt16LE()` 写入小端序）写入 `value` 到 `buf` 中指定的 `offset` 位置。
`value` 应当是一个有效的有符号的16位整数。
当 `value` 不是一个有符号的16位整数时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的最后一位字节，但后果是不确定的。

`value` 会被解析并写入为二进制补码值。

例子：

```js
const buf = Buffer.allocUnsafe(4);

buf.writeInt16BE(0x0102, 0);
buf.writeInt16LE(0x0304, 2);

// 输出: <Buffer 01 02 04 03>
console.log(buf);
```

