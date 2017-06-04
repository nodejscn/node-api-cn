<!-- YAML
added: v0.5.5
-->

* `offset` {integer} 开始读取的位置，必须满足：`0 <= offset <= buf.length - 2`
* `noAssert` {boolean} 是否跳过 `offset` 检验？**默认:** `false`
* 返回: {integer}

用指定的字节序格式（`readUInt16BE()` 返回大端序，`readUInt16LE()` 返回小端序）从 `buf` 中指定的 `offset` 读取一个无符号的16位整数值。

设置 `noAssert` 为 `true` 则 `offset` 可超出 `buf` 的最后一位字节，但后果是不确定的。

例子：

```js
const buf = Buffer.from([0x12, 0x34, 0x56]);

// 输出: 1234
console.log(buf.readUInt16BE(0).toString(16));

// 输出: 3412
console.log(buf.readUInt16LE(0).toString(16));

// 输出: 3456
console.log(buf.readUInt16BE(1).toString(16));

// 输出: 5634
console.log(buf.readUInt16LE(1).toString(16));

// 抛出异常: RangeError: Index out of range
console.log(buf.readUInt16LE(2).toString(16));
```

