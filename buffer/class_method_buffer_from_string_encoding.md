<!-- YAML
added: v5.10.0
-->

* `string` {string} 要编码的字符串
* `encoding` {string} `string` 的字符编码。 **默认:** `'utf8'`

新建一个包含所给的 JavaScript 字符串 `string` 的 `Buffer` 。
`encoding` 参数指定 `string` 的字符编码。

例子：

```js
const buf1 = Buffer.from('this is a tést');

// 输出: this is a tést
console.log(buf1.toString());

// 输出: this is a tC)st
console.log(buf1.toString('ascii'));


const buf2 = Buffer.from('7468697320697320612074c3a97374', 'hex');

// 输出: this is a tést
console.log(buf2.toString());
```

如果 `string` 不是一个字符串，则抛出 `TypeError` 错误。

