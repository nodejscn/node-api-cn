<!-- YAML
added: v6.3.0
-->

* 返回: {Buffer} `buf` 的引用。

将 `buf` 解析成 64 位数值的数组，并且以字节顺序原地进行交换。
如果 [`buf.length`] 不是 8 的倍数，则抛出 [`ERR_INVALID_BUFFER_SIZE`]。

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

console.log(buf1);
// 打印: <Buffer 01 02 03 04 05 06 07 08>

buf1.swap64();

console.log(buf1);
// 打印: <Buffer 08 07 06 05 04 03 02 01>

const buf2 = Buffer.from([0x1, 0x2, 0x3]);

buf2.swap64();
// 抛出异常 ERR_INVALID_BUFFER_SIZE。
```

JavaScript 不能编码 64 位整数。
该方法是用来处理 64 位浮点数的。

