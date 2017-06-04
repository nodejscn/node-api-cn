<!-- YAML
added: v5.3.0
-->

* `value` {string|Buffer|integer} 要搜索的值
* `byteOffset` {integer} `buf` 中开始搜索的位置。**默认:** `0`
* `encoding` {string} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {boolean} 如果 `buf` 找到 `value`，则返回 `true`，否则返回 `false`

相当于 [`buf.indexOf() !== -1`]。

例子：

```js
const buf = Buffer.from('this is a buffer');

// 输出: true
console.log(buf.includes('this'));

// 输出: true
console.log(buf.includes('is'));

// 输出: true
console.log(buf.includes(Buffer.from('a buffer')));

// 输出: true
// (97 是 'a' 的十进制 ASCII 值)
console.log(buf.includes(97));

// 输出: false
console.log(buf.includes(Buffer.from('a buffer example')));

// 输出: true
console.log(buf.includes(Buffer.from('a buffer example').slice(0, 8)));

// 输出: false
console.log(buf.includes('this', 4));
```

