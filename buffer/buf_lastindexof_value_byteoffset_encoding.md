<!-- YAML
added: v6.0.0
-->

* `value` {String | Buffer | Integer} 要搜索的值
* `byteOffset` {Integer} `buf` 中开始搜索的位置。
  **默认:** [`buf.length`]` - 1`
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
console.log(utf16Buffer.lastIndexOf('\u03a3', undefined, 'ucs2'));

// 输出: 4
console.log(utf16Buffer.lastIndexOf('\u03a3', -5, 'ucs2'));
```

If `value` is not a string, number, or `Buffer`, this method will throw a
`TypeError`. If `value` is a number, it will be coerced to a valid byte value,
an integer between 0 and 255.

If `byteOffset` is not a number, it will be coerced to a number. Any arguments
that coerce to `NaN`, like `{}` or `undefined`, will search the whole buffer.
This behavior matches [`String#lastIndexOf()`].

```js
const b = Buffer.from('abcdef');

// Passing a value that's a number, but not a valid byte
// Prints: 2, equivalent to searching for 99 or 'c'
console.log(b.lastIndexOf(99.9));
console.log(b.lastIndexOf(256 + 99));

// Passing a byteOffset that coerces to NaN
// Prints: 1, searching the whole buffer
console.log(b.lastIndexOf('b', undefined));
console.log(b.lastIndexOf('b', {}));

// Passing a byteOffset that coerces to 0
// Prints: -1, equivalent to passing 0
console.log(b.lastIndexOf('b', null));
console.log(b.lastIndexOf('b', []));
```

