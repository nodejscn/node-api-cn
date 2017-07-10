<!-- YAML
added: v1.5.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10236
    description: The `value` can now be a `Uint8Array`.
  - version: v5.7.0, v4.4.0
    pr-url: https://github.com/nodejs/node/pull/4803
    description: When `encoding` is being passed, the `byteOffset` parameter
                 is no longer required.
-->

* `value` {string|Buffer|Uint8Array|integer} 要搜索的值
* `byteOffset` {integer} `buf` 中开始搜索的位置。**默认:** `0`
* `encoding` {string} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {integer} `buf` 中 `value` 首次出现的索引，如果 `buf` 没包含 `value` 则返回 `-1`

如果 `value` 是：

  * 字符串，则 `value` 根据 `encoding` 的字符编码进行解析。
  * `Buffer` 或 [`Uint8Array`]，则 `value` 会被作为一个整体使用。如果要比较部分 `Buffer`，可使用 [`buf.slice()`]。
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

如果 `value` 不是一个字符串， 数字， 或者 `Buffer`， 该方法会抛出一个
`TypeError` 异常， 如果 `value` 是一个数字， 它将会被强制转换成一个有效的 byte 值，
该值介于0到255之间。

如果 `byteOffset` 不是一个数字， 它将会被强制转换成一个数字。  任何对 `NaN` or 0, like `{}`, `[]`, `null` or `undefined`，
的参数， 将会搜索整个 buffer。 该行为和 [`String#indexOf()`] 保持一致。

```js
const b = Buffer.from('abcdef');

// 传入一个不是有效字节的数字
// 输出：2，相当于搜索 99 或 'c'
console.log(b.indexOf(99.9));
console.log(b.indexOf(256 + 99));

// 传入 byteOffset，其值强制转换为 NaN 或 0
// 输出：1，搜索整个 buffer
console.log(b.indexOf('b', undefined));
console.log(b.indexOf('b', {}));
console.log(b.indexOf('b', null));
console.log(b.indexOf('b', []));
```

如果 `value` 是一个空字符串或空 `Buffer`，并且 `byteOffset` 小于 `buf.length`，返回 `byteOffset`。如果 `value` 是一个空字符串，并且 `byteOffset` 大于 `buf.length`，返回 `buf.length`。
