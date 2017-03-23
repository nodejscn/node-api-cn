<!-- YAML
added: v1.5.0
-->

* `value` {String | Buffer | Integer} 要搜索的值
* `byteOffset` {Integer} `buf` 中开始搜索的位置。**默认:** `0`
* `encoding` {String} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {Integer} `buf` 中 `value` 首次出现的索引，如果 `buf` 没包含 `value` 则返回 `-1`

如果 `value` 是：

  * 字符串，则 `value` 根据 `encoding` 的字符编码进行解析。
  * `Buffer`，则 `value` 会被作为一个整体使用。如果要比较部分 `Buffer` 可使用 [`buf.slice()`]。
  * 数值, 则 `value` 会解析为一个 `0` 至 `255` 之间的无符号八位整数值。

例子：

```js
const buf = Buffer.from('this is a buffer');

// 输出: 0
console.log(buf.indexOf('this'));

// 输出: 2
console.log(buf.indexOf('is'));

// 输出: 8
console.log(buf.indexOf(Buffer.from('a buffer')));

// 输出: 8
// (97 是 'a' 的十进制 ASCII 值)
console.log(buf.indexOf(97));

// 输出: -1
console.log(buf.indexOf(Buffer.from('a buffer example')));

// 输出: 8
console.log(buf.indexOf(Buffer.from('a buffer example').slice(0, 8)));


const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'ucs2');

// 输出: 4
console.log(utf16Buffer.indexOf('\u03a3', 0, 'ucs2'));

// 输出: 6
console.log(utf16Buffer.indexOf('\u03a3', -4, 'ucs2'));
```

If `value` is not a string, number, or `Buffer`, this method will throw a
`TypeError`. If `value` is a number, it will be coerced to a valid byte value,
an integer between 0 and 255.

If `byteOffset` is not a number, it will be coerced to a number. Any arguments
that coerce to `NaN` or 0, like `{}`, `[]`, `null` or `undefined`, will search
the whole buffer. This behavior matches [`String#indexOf()`].

```js
const b = Buffer.from('abcdef');

// Passing a value that's a number, but not a valid byte
// Prints: 2, equivalent to searching for 99 or 'c'
console.log(b.indexOf(99.9));
console.log(b.indexOf(256 + 99));

// Passing a byteOffset that coerces to NaN or 0
// Prints: 1, searching the whole buffer
console.log(b.indexOf('b', undefined));
console.log(b.indexOf('b', {}));
console.log(b.indexOf('b', null));
console.log(b.indexOf('b', []));
```

