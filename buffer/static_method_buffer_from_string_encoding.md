<!-- YAML
added: v5.10.0
-->

* `string` {string} 要编码的字符串。
* `encoding` {string} `string` 的字符编码。**默认值:** `'utf8'`。

创建一个包含 `string` 的新 `Buffer`。
`encoding` 参数指定用于将 `string` 转换为字节的字符编码。

```js
const buf1 = Buffer.from('this is a tést');
const buf2 = Buffer.from('7468697320697320612074c3a97374', 'hex');

console.log(buf1.toString());
// 打印: this is a tést
console.log(buf2.toString());
// 打印: this is a tést
console.log(buf1.toString('latin1'));
// 打印: this is a tÃ©st
```

如果 `string` 不是一个字符串或适用于 `Buffer.from()` 变量的其他类型，则抛出 `TypeError`。

