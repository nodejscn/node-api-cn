<!-- YAML
added: v0.11.15
-->

* `value` {number} 要写入 `buf` 的数值
* `offset` {integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - 8`
* `noAssert` {boolean} 是否跳过 `value` 和 `offset` 检验？**默认:** `false`
* 返回: {integer} `offset` 加上写入的字节数

用指定的字节序格式（`writeDoubleBE()` 写入大端序，`writeDoubleLE()` 写入小端序）写入 `value` 到 `buf` 中指定的 `offset` 位置。
`value` 应当是一个有效的64位双精度值。
当 `value` 不是一个64位双精度值时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的最后一位字节，但后果是不确定的。

例子：

```js
const buf = Buffer.allocUnsafe(8);

buf.writeDoubleBE(0xdeadbeefcafebabe, 0);

// 输出: <Buffer 43 eb d5 b7 dd f9 5f d7>
console.log(buf);

buf.writeDoubleLE(0xdeadbeefcafebabe, 0);

// 输出: <Buffer d7 5f f9 dd b7 d5 eb 43>
console.log(buf);
```

