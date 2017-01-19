<!-- YAML
added: v0.11.15
-->

* `offset` {Integer} 开始读取的位置，必须满足：`0 <= offset <= buf.length - 8`
* `noAssert` {Boolean} 是否跳过 `offset` 检验？**默认:** `false`
* 返回: {Number}

用指定的尾数格式（`readDoubleBE()` 返回大尾数，`readDoubleLE()` 返回小尾数）从 `buf` 中指定的 `offset` 读取一个64位双精度值。

设置 `noAssert` 为 `true` 则 `offset` 可超出 `buf` 的末尾，但后果是不确定的。

例子：

```js
const buf = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8]);

// 输出: 8.20788039913184e-304
console.log(buf.readDoubleBE());

// 输出: 5.447603722011605e-270
console.log(buf.readDoubleLE());

// 抛出异常: RangeError: Index out of range
console.log(buf.readDoubleLE(1));

// 警告: 读取超出 buffer 的末尾！
// 这会导致内存区段错误！不要这么做！
console.log(buf.readDoubleLE(1, true));
```

