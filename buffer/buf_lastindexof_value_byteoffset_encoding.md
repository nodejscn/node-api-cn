<!-- YAML
added: v6.0.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10236
    description: The `value` can now be a `Uint8Array`.
-->

* `value` {string|Buffer|Uint8Array|integer} 要搜索的值
* `byteOffset` {integer} `buf` 中开始搜索的位置。
  **默认:** [`buf.length`]` - 1`
* `encoding` {string} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {integer} `buf` 中 `value` 最后一次出现的索引，如果 `buf` 没包含 `value` 则返回 `-1`

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

如果 `value` 不是一个字符串， 数字， 或者 `Buffer`， 该方法会抛出一个
`TypeError` 异常， 如果 `value` 是一个数字， 它将会被强制转换成一个有效的 byte 值，
该值介于0到255之间。

如果 `byteOffset` 不是一个数字， 它将会被强制转换成一个数字。  任何对 `NaN` or 0, like `{}`, `[]`, `null` or `undefined`，
的参数， 将会搜索整个 buffer。 该行为和 [`String#lastIndexOf()`] 保持一致。

```js
const b = Buffer.from('abcdef');

// 传入一个不是有效字节的数字
// 输出：2，相当于搜索 99 或 'c'
console.log(b.lastIndexOf(99.9));
console.log(b.lastIndexOf(256 + 99));

// 传入 byteOffset，其值强制转换为 NaN
// 输出：1，搜索整个 buffer
console.log(b.lastIndexOf('b', undefined));
console.log(b.lastIndexOf('b', {}));

// 传入 byteOffset，其值强制转换为 0
// 输出：-1，相当于传入 0
console.log(b.lastIndexOf('b', null));
console.log(b.lastIndexOf('b', []));
```

如果 `value` 是一个空字符串或者空 `Buffer`，返回 `byteOffset`。
