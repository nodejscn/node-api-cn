<!-- YAML
added: v5.10.0
-->

* `buffer` {Buffer|Uint8Array} 要拷贝数据的 `Buffer` 或 [`Uint8Array`]。

拷贝 `buffer` 的数据到新建的 `Buffer` 实例。

```js
const buf1 = Buffer.from('buffer');
const buf2 = Buffer.from(buf1);

buf1[0] = 0x61;

console.log(buf1.toString());
// 打印: auffer
console.log(buf2.toString());
// 打印: buffer
```

如果 `buffer` 不是一个 `Buffer` 或适用于 `Buffer.from()` 变量的其他类型，则抛出 `TypeError`。

