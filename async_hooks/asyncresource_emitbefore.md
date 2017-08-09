
* 返回 {undefined}

调用所有`before`回调，并且让他们知道正在输入一个新的异步执行上下文。 如果对`emitBefore()`进行嵌套调用，那么将会跟踪并正确地解开`asyncId`的堆栈。
