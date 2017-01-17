<!-- YAML
added: v5.10.0
-->

* `buffer` {Buffer} 一个要拷贝数据的已存在的 `Buffer`

将传入的 `buffer` 数据拷贝到一个新建的 `Buffer` 实例。

例子：

```js
const buf1 = Buffer.from('buffer');
const buf2 = Buffer.from(buf1);

buf1[0] = 0x61;

// 输出: auffer
console.log(buf1.toString());

// 输出: buffer
console.log(buf2.toString());
```

如果 `buffer` 不是一个 `Buffer`，则抛出 `TypeError` 错误。

