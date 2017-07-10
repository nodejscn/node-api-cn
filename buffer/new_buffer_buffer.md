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

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(buffer)`] 代替。

* `buffer` {Buffer} 一个要拷贝数据的已存在的 `Buffer`

将传入的 `buffer` 数据拷贝到一个新建的 `Buffer` 实例。

例子:

```js
const buf1 = new Buffer('buffer');
const buf2 = new Buffer(buf1);

buf1[0] = 0x61;

// 输出: auffer
console.log(buf1.toString());

// Prints: buffer
console.log(buf2.toString());
```
