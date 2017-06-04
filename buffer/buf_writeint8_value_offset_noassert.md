<!-- YAML
added: v0.5.0
-->

* `value` {integer} 要写入 `buf` 的数值
* `offset` {integer} 开始写入的位置，必须满足：`0 <= offset <= buf.length - 1`
* `noAssert` {boolean} 是否跳过 `value` 和 `offset` 检验？**默认:** `false`
* 返回: {integer} `offset` 加上写入的字节数

写入 `value` 到 `buf` 中指定的 `offset` 位置。
`value` 应当是一个有效的有符号的8位整数。
当 `value` 不是一个有符号的8位整数时，反应是不确定的。

设置 `noAssert` 为 `true` 则 `value` 的编码形式可超出 `buf` 的末尾，但后果是不确定的。

`value` 会被解析并写入为二进制补码值。

例子：

```js
const buf = Buffer.allocUnsafe(2);

buf.writeInt8(2, 0);
buf.writeInt8(-2, 1);

// 输出: <Buffer 02 fe>
console.log(buf);
```

