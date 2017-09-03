<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.allocUnsafeSlow()`] 代替。

* `size` {integer} 新建的 `SlowBuffer` 期望的长度

分配一个 `size` 字节的新的 `Buffer`。如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，将会抛出 [`RangeError`] 错误。如果 `size` 为 0，则返回一个为 0 的 `Buffer`.

`SlowBuffer` 实例的底层内存是 *未初始化的*。新建的 `SlowBuffer` 的内容是未知的，并且可能包含敏感数据。使用 [`buf.fill(0)`][`buf.fill()`] 初始化 `SlowBuffer` 为 0。

例子:

```js
const { SlowBuffer } = require('buffer');

const buf = new SlowBuffer(5);

// 输出: (内容可能有变化): <Buffer 78 e0 82 02 01>
console.log(buf);

buf.fill(0);

// 输出: <Buffer 00 00 00 00 00>
console.log(buf);
```
