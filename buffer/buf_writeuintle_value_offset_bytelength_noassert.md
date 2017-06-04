<!-- YAML
added: v0.5.5
-->

* `value` {integer} 要写入 `buf` 的数值
* `offset` {integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - byteLength`
* `byteLength` {integer} 要写入的字节数，必须满足：`0 < byteLength <= 6`
* `noAssert` {boolean} 是否跳过 `value`、`offset` 和 `byteLength` 检验？**默认:** `false`
* 返回: {integer} `offset` 加上写入的字节数

写入 `value` 中的 `byteLength` 个字节到 `buf` 中指定的 `offset` 位置。
最高支持48位精度。
当 `value` 不是一个无符号的整数时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的末尾，但后果是不确定的。

例子：

```js
const buf = Buffer.allocUnsafe(6);

buf.writeUIntBE(0x1234567890ab, 0, 6);

// 输出: <Buffer 12 34 56 78 90 ab>
console.log(buf);

buf.writeUIntLE(0x1234567890ab, 0, 6);

// 输出: <Buffer ab 90 78 56 34 12>
console.log(buf);
```

