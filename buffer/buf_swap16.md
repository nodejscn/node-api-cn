<!-- YAML
added: v5.10.0
-->

* 返回: {Buffer} `buf` 的引用

将 `buf` 解析为一个无符号16位的整数数组，并且以字节顺序原地进行交换。
如果 [`buf.length`] 不是2的倍数，则抛出 `RangeError` 错误。

例子：

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

// 输出: <Buffer 01 02 03 04 05 06 07 08>
console.log(buf1);

buf1.swap16();

// 输出: <Buffer 02 01 04 03 06 05 08 07>
console.log(buf1);


const buf2 = Buffer.from([0x1, 0x2, 0x3]);

// 抛出异常: RangeError: Buffer size must be a multiple of 16-bits
buf2.swap16();
```

