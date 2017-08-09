<!-- YAML
added: v0.5.0
changes:
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4935
    description: The `encoding` parameter is supported now.
-->

* `value` {string|Buffer|integer} 用来填充 `buf` 的值
* `offset` {integer} 开始填充 `buf` 的位置。**默认:** `0`
* `end` {integer} 结束填充 `buf` 的位置（不包含）。**默认:** [`buf.length`]
* `encoding` {string} 如果 `value` 是一个字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {Buffer} `buf` 的引用

如果未指定 `offset` 和 `end`，则填充整个 `buf`。
这个简化使得一个 `Buffer` 的创建与填充可以在一行内完成。

例子：用 ASCII 字符 `'h'` 填充 `Buffer`。

```js
const b = Buffer.allocUnsafe(50).fill('h');

// 输出: hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh
console.log(b.toString());
```

`value` 如果不是一个字符串或整数，则会被强行转换为 `uint32` 值。

如果 `fill()` 操作的最后一次写入的是一个多字节字符，则只有字符中适合 `buf` 的第一个字节会被写入。

例子：用一个两个字节的字符填充 `Buffer`。

```js
// 输出: <Buffer c8 a2 c8>
console.log(Buffer.allocUnsafe(3).fill('\u0222'));
```

