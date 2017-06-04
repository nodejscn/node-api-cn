
* `message` {string}

新建一个 `Error` 实例，并设置 `error.message` 属性以提供文本信息。
如果 `message` 传的是一个对象，则会调用 `message.toString()` 生成文本信息。
`error.stack` 属性表示被调用的 `new Error()` 在代码中的位置。
堆栈跟踪是基于 [V8 的堆栈跟踪 API] 的。
堆栈跟踪只会取（a）异步代码执行的开头或（b）`Error.stackTraceLimit` 属性给出的栈帧中的最小项。

