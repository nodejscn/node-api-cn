
* {number}

`Error.stackTraceLimit` 属性指定了堆栈跟踪收集的栈帧数量（无论是 `new Error().stack` 或 `Error.captureStackTrace(obj)` 产生的）。

默认值为 `10` ，但可设为任何有效的 JavaScript 数值。
值改变后的变化会影响所有捕获到的堆栈跟踪。

如果设为一个非数值或负数，则堆栈跟踪不会捕捉任何栈帧。

