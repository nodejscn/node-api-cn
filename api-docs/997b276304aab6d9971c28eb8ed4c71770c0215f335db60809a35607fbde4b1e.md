
<!--type=misc-->

JavaScript 异常是一个作为一个无效操作的结果或作为一个 `throw` 声明的目标所抛出的值。
虽然它不要求这些值是 `Error` 的实例或继承自 `Error` 的类的实例，但所有通过 Node.js 或 JavaScript 运行时抛出的异常都是 `Error` 实例。

有些异常在 JavaScript 层是无法恢复的。
这些异常总会引起 Node.js 进程的崩溃。
例如 `assert()` 检测或在 C++ 层调用的 `abort()`。

