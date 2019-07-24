<!-- YAML
added: v5.10.0
-->

* 返回: {Buffer} `buf` 的引用。

将 `buf` 解析成无符号的 16 位整数的数组，并且以字节顺序原地进行交换。
如果 [`buf.length`] 不是 2 的倍数，则抛出 [`ERR_INVALID_BUFFER_SIZE`]。

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

console.log(buf1);
// 打印: <Buffer 01 02 03 04 05 06 07 08>

buf1.swap16();

console.log(buf1);
// 打印: <Buffer 02 01 04 03 06 05 08 07>

const buf2 = Buffer.from([0x1, 0x2, 0x3]);

buf2.swap16();
// 抛出异常 ERR_INVALID_BUFFER_SIZE。
```

`buf.swap16()` 的一个方便用途是在 UTF-16 小端序和 UTF-16 大端序之间执行快速的原地转换：

```js
const buf = Buffer.from('This is little-endian UTF-16', 'utf16le');
buf.swap16(); // 转换为大端序 UTF-16 文本。
```
