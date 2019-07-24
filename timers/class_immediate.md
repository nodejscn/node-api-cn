
此对象在内部创建，并从 [`setImmediate()`] 返回。 
它可以传给 [`clearImmediate()`] 以取消计划的操作。

默认情况下，当预定 immediate 时，只要 immediate 激活，Node.js 事件循环将继续运行。 
[`setImmediate()`] 返回的 `Immediate` 对象导出 `immediate.ref()` 和 `immediate.unref()` 函数，这些函数可用于控制此默认行为。

