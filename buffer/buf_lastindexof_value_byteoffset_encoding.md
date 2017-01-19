<!-- YAML
added: v6.0.0
-->

* `value` {String | Buffer | Integer} 要搜索的值
* `byteOffset` {Integer} `buf` 中开始搜索的位置（不包含）。
  **默认:** [`buf.length`]
* `encoding` {String} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {Integer} `buf` 中 `value` 最后一次出现的索引，如果 `buf` 没包含 `value` 则返回 `-1`

与 [`buf.indexOf()`] 类似，除了 `buf` 是从后往前搜索而不是从前往后。

例子：

```js
const buf = Buffer.from('this buffer is a buffer');

// 输出: 0
console.log(buf.lastIndexOf('this'));

// 输出: 17
console.log(buf.lastIndexOf('buffer'));

// 输出: 17
console.log(buf.lastIndexOf(Buffer.from('buffer')));

// 输出: 15
// (97 是 'a' 的十进制 ASCII 值)
console.log(buf.lastIndexOf(97));

// 输出: -1
console.log(buf.lastIndexOf(Buffer.from('yolo')));

// 输出: 5
console.log(buf.lastIndexOf('buffer', 5));

// 输出: -1
console.log(buf.lastIndexOf('buffer', 4));


const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'ucs2');

// 输出: 6
console.log(utf16Buffer.lastIndexOf('\u03a3', null, 'ucs2'));

// 输出: 4
console.log(utf16Buffer.lastIndexOf('\u03a3', -5, 'ucs2'));
```

