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

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(array)`] 代替。

* `array` {Array} 要从中复制的字节数组

使用八字节的 `array` 分配一个新的 `Buffer`。

例子:

```js
// 创建一个新的包含字符串 'buffer' 的 UTF-8 编码的 Buffer
const buf = new Buffer([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```
