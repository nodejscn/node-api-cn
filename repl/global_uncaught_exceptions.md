
REPL使用 [`domain`](http://nodejs.cn/s/cnfQ9s) 模块来捕获会话期间的所有未捕获异常。

在REPL中使用 [`domain`](http://nodejs.cn/s/cnfQ9s) 模块有如下副作用：

* 未捕获的异常不会产生 [`uncaughtException`](http://nodejs.cn/s/Lc6A38) 事件。
* 如果尝试使用 [`process.setUncaughtExceptionCaptureCallback()`](http://nodejs.cn/s/4yit6t) 将产生一个 [`ERR_DOMAIN_CANNOT_SET_UNCAUGHT_EXCEPTION_CAPTURE`](http://nodejs.cn/s/3Hg5uo) 错误。

