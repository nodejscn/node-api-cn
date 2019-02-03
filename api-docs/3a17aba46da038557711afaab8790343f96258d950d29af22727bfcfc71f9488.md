
此对象在内部创建，并从 [`setTimeout()`] 和 [`setInterval()`] 返回。 
它可以传给 [`clearTimeout()`] 或 [`clearInterval()`] 以取消计划的操作。

默认情况下，当使用 [`setTimeout()`] 或 [`setInterval()`] 预定定时器时，只要定时器处于活动状态，Node.js 事件循环将继续运行。 
这些函数返回的每个 `Timeout` 对象都会导出 `timeout.ref()` 和 `timeout.unref()` 函数，这些函数可用于控制此默认行为。


