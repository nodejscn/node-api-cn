<!-- YAML
added: v6.3.0
-->

* 返回: {Buffer} `buf` 的引用

将 `buf` 解析为一个64位的数值数组，并且以字节顺序原地进行交换。
如果 [`buf.length`] 不是8的倍数，则抛出 `RangeError` 错误。

例子：

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

// 输出: <Buffer 01 02 03 04 05 06 07 08>
console.log(buf1);

buf1.swap64();

// 输出: <Buffer 08 07 06 05 04 03 02 01>
console.log(buf1);


const buf2 = Buffer.from([0x1, 0x2, 0x3]);

// 抛出异常: RangeError: Buffer size must be a multiple of 64-bits
buf2.swap64();
```

注意，JavaScript 不能编码64位整数。
该方法是用来处理64位浮点数的。

