
正常情况下，如果没有异步操作正在等待，那么Node.js会以状态码`0`退出，其他情况下，会
用如下的状态码:

* `1` **未捕获异常** - 有一个未被捕获的异常,
  并且没被一个 domain 或 an [`'uncaughtException'`][] 事件处理器处理。
* `2` - 未被使用 (Bash为防内部滥用而保留)
* `3` **内部JavaScript 分析错误** - Node.js的内部的JavaScript源代码
  在引导进程中导致了一个语法分析错误。
  这是非常少见的, 一般只会在开发Node.js本身的时候出现。
* `4` **内部JavaScript执行失败** - 
  引导进程执行Node.js的内部的JavaScript源代码时，返回函数值失败。
  这是非常少见的, 一般只会在开发Node.js本身的时候出现。
* `5` **致命错误** - 在V8中有一个致命的错误.
  比较典型的是以`FATALERROR`为前缀从stderr打印出来的消息。
* `6` **非函数的内部异常处理** - 发生了一个内部异常，但是内部异常处理函数
  被设置成了一个非函数，或者不能被调用。
* `7` **内部异常处理运行时失败** - 有一个不能被捕获的异常。
  在试图处理这个异常时，处理函数本身抛出了一个错误。
  这是可能发生的, 比如, 如果一个 [`'uncaughtException'`][] 或者
  `domain.on('error')` 处理函数抛出了一个错误。
* `8` - 未被使用.  在之前版本的Node.js, 退出码8有时候表示一个未被捕获的异常。
* `9` - **不可用参数** - 也许是某个未知选项没有确定，或者没给必需要的选项填值。
* `10` **内部JavaScript运行时失败** - 调用引导函数时，
  引导进程执行Node.js的内部的JavaScript源代码抛出错误。
  这是非常少见的, 一般只会在开发Node.js本身的时候出现。
* `12` **不可用的调试参数** - The `--inspect` and/or `--inspect-brk`
  options were set, but the port number chosen was invalid or unavailable.
* `>128` **退出信号** - If Node.js receives a fatal signal such as
  `SIGKILL` or `SIGHUP`, then its exit code will be `128` plus the
  value of the signal code.  This is a standard POSIX practice, since
  exit codes are defined to be 7-bit integers, and signal exits set
  the high-order bit, and then contain the value of the signal code.
