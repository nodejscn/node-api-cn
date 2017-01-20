<!-- YAML
added: v0.5.5
-->

* `value` {Integer} 要写入 `buf` 的数值
* `offset` {Integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - 2`
* `noAssert` {Boolean} 是否跳过 `value` 和 `offset` 检验？**默认:** `false`
* 返回: {Integer} `offset` 加上写入的字节数

用指定的尾数格式（`writeUInt16BE()` 写入大尾数，`writeUInt16LE()` 写入小尾数）写入 `value` 到 `buf` 中指定的 `offset` 位置。
`value` 应当是一个有效的无符号的16位整数。
当 `value` 不是一个无符号的16位整数时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的末尾，但后果是不确定的。

例子：

```js
const buf = Buffer.allocUnsafe(4);

buf.writeUInt16BE(0xdead, 0);
buf.writeUInt16BE(0xbeef, 2);

// 输出: <Buffer de ad be ef>
console.log(buf);

buf.writeUInt16LE(0xdead, 0);
buf.writeUInt16LE(0xbeef, 2);

// 输出: <Buffer ad de ef be>
console.log(buf);
```

