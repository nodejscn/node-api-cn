<!-- YAML
added: v0.5.0
-->

* `offset` {integer} 开始读取的位置，必须满足：`0 <= offset <= buf.length - 1`
* `noAssert` {boolean} 是否跳过 `offset` 检验？**默认:** `false`
* 返回: {integer}

从 `buf` 中指定的 `offset` 读取一个有符号的8位整数值。

设置 `noAssert` 为 `true` 则 `offset` 可超出 `buf` 的最后一位字节，但后果是不确定的。

从 `Buffer` 中读取的整数值会被解析为二进制补码值。

例子：

```js
const buf = Buffer.from([-1, 5]);

// 输出: -1
console.log(buf.readInt8(0));

// 输出: 5
console.log(buf.readInt8(1));

// 抛出异常: RangeError: Index out of range
console.log(buf.readInt8(2));
```

