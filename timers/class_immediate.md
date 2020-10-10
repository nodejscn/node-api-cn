
此对象在 [`setImmediate()`] 内部创建并返回。 
它可以传给 [`clearImmediate()`] 以取消已安排的行动。

默认情况下，当一个 immediate 被安排时，只要 immediate 处于活动状态，则 Node.js 事件循环就会继续运行。 
[`setImmediate()`] 返回的 `Immediate` 对象会导出 `immediate.ref()` 和 `immediate.unref()` 函数，可用于控制此默认的行为。

