<!-- YAML
added: v5.10.0
-->

* 返回: {Buffer} `buf` 的引用。

将 `buf` 解析成无符号的 32 位整数的数组，并且以字节顺序原地进行交换。
如果 [`buf.length`] 不是 4 的倍数，则抛出 [`ERR_INVALID_BUFFER_SIZE`]。

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

console.log(buf1);
// 打印: <Buffer 01 02 03 04 05 06 07 08>

buf1.swap32();

console.log(buf1);
// 打印: <Buffer 04 03 02 01 08 07 06 05>

const buf2 = Buffer.from([0x1, 0x2, 0x3]);

buf2.swap32();
// 抛出异常 ERR_INVALID_BUFFER_SIZE。
```

