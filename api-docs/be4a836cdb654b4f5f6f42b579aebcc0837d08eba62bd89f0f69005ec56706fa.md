<!-- YAML
added: v5.10.0
-->

* `string` {string} 要编码的字符串。
* `encoding` {string} `string` 的字符编码。默认为 `'utf8'`。

创建一个包含 `string` 的 `Buffer`。

```js
const buf1 = Buffer.from('this is a tést');
const buf2 = Buffer.from('7468697320697320612074c3a97374', 'hex');

console.log(buf1.toString());
// 输出: this is a tést
console.log(buf2.toString());
// 输出: this is a tést
console.log(buf1.toString('ascii'));
// 输出: this is a tC)st
```

