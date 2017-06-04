<!-- YAML
added: v0.11.15
-->

* `offset` {integer} 开始读取的位置，必须满足：`0 <= offset <= buf.length - 4`
* `noAssert` {boolean} 是否跳过 `offset` 检验？**默认:** `false`
* 返回: {number}

用指定的字节序格式（`readFloatBE()` 返回大端序，`readFloatLE()` 返回小端序）从 `buf` 中指定的 `offset` 读取一个32位浮点值。

设置 `noAssert` 为 `true` 则 `offset` 可超出 `buf` 的最后一位字节，但后果是不确定的。

例子：

```js
const buf = Buffer.from([1, 2, 3, 4]);

// 输出: 2.387939260590663e-38
console.log(buf.readFloatBE());

// 输出: 1.539989614439558e-36
console.log(buf.readFloatLE());

// 抛出异常: RangeError: Index out of range
console.log(buf.readFloatLE(1));

// 警告: 读取超出 buffer 的最后一位字节！
// 这会导致内存区段错误！不要这么做！
console.log(buf.readFloatLE(1, true));
```

