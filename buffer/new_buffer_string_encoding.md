<!-- YAML
deprecated: v6.0.0
changes:
  - version: v7.2.1
    pr-url: https://github.com/nodejs/node/pull/9529
    description: Calling this constructor no longer emits a deprecation warning.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8169
    description: Calling this constructor emits a deprecation warning now.
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(string[, encoding])`][`Buffer.from(string)`] 代替。

* `string` {string} 要编码的字符串
* `encoding` {string} `string` 的字符串编码。 **默认：** `'utf8'`

创建一个包含给定字符串 `string` 的 `Buffer`。`encoding` 参数制定 `string` 的字符串编码。

例子:

```js
const buf1 = new Buffer('this is a tést');

// 输出: this is a tést
console.log(buf1.toString());

// 输出: this is a tC)st
console.log(buf1.toString('ascii'));


const buf2 = new Buffer('7468697320697320612074c3a97374', 'hex');

// 输出: this is a tést
console.log(buf2.toString());
```
