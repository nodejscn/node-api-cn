
* 返回 {undefined}

调用所有`after`回调。 如果对`emitBefore()`进行嵌套调用，那么请确保堆栈被正确释放。否则将会抛出错误。

如果用户的回调抛出异常并且错误由域或`'uncaughtException'`句柄处理，那么将会为所有堆栈上的`asyncId`自动调用`emitAfter()`。

