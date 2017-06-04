<!-- YAML
added: v0.11.15
-->

* `offset` {integer} 开始读取的位置，必须满足：`0 <= offset <= buf.length - byteLength`
* `byteLength` {integer} 要读取的字节数。必须满足：`0 < byteLength <= 6`
* `noAssert` {boolean} 是否跳过 `offset` 和 `byteLength` 校验？ **默认:** `false`
* 返回: {integer}

从 `buf` 中指定的 `offset` 读取 `byteLength` 个字节，且读取的值会被解析为二进制补码值。
最高支持48位精度。

设置 `noAssert` 为 `true` 则 `offset` 可超出 `buf` 的最后一位字节，但后果是不确定的。

例子：

```js
const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

// 输出: -546f87a9cbee
console.log(buf.readIntLE(0, 6).toString(16));

// 输出: 1234567890ab
console.log(buf.readIntBE(0, 6).toString(16));

// 抛出异常: RangeError: Index out of range
console.log(buf.readIntBE(1, 6).toString(16));
```

