<!-- YAML
deprecated: v6.0.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12141
    description: new Buffer(size) will return zero-filled memory by default.
  - version: v7.2.1
    pr-url: https://github.com/nodejs/node/pull/9529
    description: Calling this constructor no longer emits a deprecation warning.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8169
    description: Calling this constructor emits a deprecation warning now.
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.alloc()`] 代替（或 [`Buffer.allocUnsafe()`]）。

* `size` {integer} 新建的 `Buffer` 期望的长度

分配一个大小为 `size` 字节的新建的 `Buffer`。如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`RangeError`] 错误。如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

在 Node.js 8.0.0 之前，以这种方式创建的 `Buffer` 实例的底层内存是 *未初始化* 的。新建的 `Buffer` 的内容是未知的并且 *可能包含敏感数据*。使用 [`Buffer.alloc(size)`][`Buffer.alloc()`] 代替它去初始化 `Buffer` 为 0。

例子:

```js
const buf = new Buffer(10);

// 输出: <Buffer 00 00 00 00 00 00 00 00 00 00>
console.log(buf);
```
