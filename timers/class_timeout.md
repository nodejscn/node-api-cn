
此对象在 [`setTimeout()`] 和 [`setInterval()`] 内部创建并返回。 
它可以传给 [`clearTimeout()`] 或 [`clearInterval()`] 以取消已安排的行动。

默认情况下，当使用 [`setTimeout()`] 或 [`setInterval()`] 安排一个定时器时，只要定时器处于活动状态，则 Node.js 事件循环就会继续运行。 
这些函数返回的每个 `Timeout` 对象都会导出 `timeout.ref()` 和 `timeout.unref()` 函数，可用于控制此默认的行为。


