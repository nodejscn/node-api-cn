
该对象是内部创建的，并从 [`setTimeout()`] 和 [`setInterval()`] 返回。
它可以传给 [`clearTimeout()`] 或 [`clearInterval()`] 以便取消预定的动作。

默认情况下，当使用 [`setTimeout()`] 或 [`setInterval()`] 预定一个定时器时，只要定时器处于活动状态，Node.js 事件循环就会继续运行。
每个由这些函数返回的 `Timeout` 对象都导出了可用于控制这个默认行为的 `timeout.ref()` 和 `timeout.unref()` 函数。

