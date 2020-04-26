<!-- YAML
added: v5.10.0
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7079
    description: Passing a negative `size` will now throw an error.
-->

* `size` {integer} 新建的 `Buffer` 的长度。

创建一个大小为 `size` 字节的新 `Buffer`。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`ERR_INVALID_OPT_VALUE`]。

以这种方式创建的 `Buffer` 实例的底层内存是未初始化的。
新创建的 `Buffer` 的内容是未知的，可能包含敏感数据。
使用 [`Buffer.alloc()`] 可以创建以零初始化的 `Buffer` 实例。

```js
const buf = Buffer.allocUnsafe(10);

console.log(buf);
// 打印（内容可能有所不同）: <Buffer a0 8b 28 3f 01 00 00 00 50 32>

buf.fill(0);

console.log(buf);
// 打印: <Buffer 00 00 00 00 00 00 00 00 00 00>
```

如果 `size` 不是一个数字，则抛出 `TypeError`。

`Buffer` 模块会预分配一个内部的大小为 [`Buffer.poolSize`] 的 `Buffer` 实例，作为快速分配的内存池，用于使用 [`Buffer.allocUnsafe()`] 创建新的 `Buffer` 实例、或 [`Buffer.from(array)`]、或弃用的 `new Buffer(size)` 构造器但仅当 `size` 小于或等于 `Buffer.poolSize >> 1`（[`Buffer.poolSize`] 除以二再向下取整）。

对这个预分配的内部内存池的使用是调用 `Buffer.alloc(size, fill)` 和 `Buffer.allocUnsafe(size).fill(fill)` 两者之间的关键区别。
具体来说，`Buffer.alloc(size, fill)` 永远不会使用内部的 `Buffer` 池，而 `Buffer.allocUnsafe(size).fill(fill)` 在 `size` 小于或等于 [`Buffer.poolSize`] 的一半时将会使用内部的 `Buffer`池。
该差异虽然很微妙，但当应用程序需要 [`Buffer.allocUnsafe()`] 提供的额外性能时，则非常重要。

