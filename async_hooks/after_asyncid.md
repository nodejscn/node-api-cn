
* `asyncId` {number}

规定`before`完成后立即调用的回调

*请注意:* 如果在回调执行期间，出现未捕获异常，那么将会在触发`'uncaughtException'`事件后或`domain`句柄运行后运行`after`。

