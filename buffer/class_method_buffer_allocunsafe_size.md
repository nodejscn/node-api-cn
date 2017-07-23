<!-- YAML
added: v5.10.0
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7079
    description: Passing a negative `size` will now throw an error.
-->

* `size` {integer} 新建的 `Buffer` 期望的长度

分配一个大小为 `size` 字节的新建的 `Buffer` 。
如果 `size` 大于 [`buffer.constants.MAX_LENGTH`] 或小于 0，则抛出 [`RangeError`] 错误。
如果 `size` 为 0，则创建一个长度为 0 的 `Buffer`。

以这种方式创建的 `Buffer` 实例的底层内存是**未初始化**的。
新创建的 `Buffer` 的内容是未知的，且**可能包含敏感数据**。
可以使用 [`buf.fill(0)`] 初始化 `Buffer` 实例为0。

例子：

```js
const buf = Buffer.allocUnsafe(10);

// 输出: (内容可能不同): <Buffer a0 8b 28 3f 01 00 00 00 50 32>
console.log(buf);

buf.fill(0);

// 输出: <Buffer 00 00 00 00 00 00 00 00 00 00>
console.log(buf);
```

如果 `size` 不是一个数值，则抛出 `TypeError` 错误。

注意，`Buffer` 模块会预分配一个大小为 [`Buffer.poolSize`] 的内部 `Buffer` 实例作为快速分配池，
用于使用 [`Buffer.allocUnsafe()`] 新创建的 `Buffer` 实例，以及废弃的 `new Buffer(size)` 构造器，
仅限于当 `size` 小于或等于 `Buffer.poolSize >> 1` （[`Buffer.poolSize`] 除以2后的最大整数值）。

对这个预分配的内部内存池的使用，是调用 `Buffer.alloc(size, fill)` 和 `Buffer.allocUnsafe(size).fill(fill)` 的关键区别。
具体地说，如果 `size` 小于或等于 [`Buffer.poolSize`] 的一半，则 `Buffer.alloc(size, fill)` **不会**使用这个内部的 `Buffer` 池，而 `Buffer.allocUnsafe(size).fill(fill)` **会**使用这个内部的 `Buffer` 池。
当应用程序需要 [`Buffer.allocUnsafe()`] 提供额外的性能时，这个细微的区别是非常重要的。

