<!-- YAML
added: v0.0.1
-->

* `callback` {Function} 当定时器到点时要调用的函数。
* `delay` {number} 调用 `callback` 之前要等待的毫秒数。
* `...args` {any} 当调用 `callback` 时要传入的可选参数。

预定每隔 `delay` 毫秒重复执行的 `callback`。
返回一个用于 [`clearInterval()`] 的 `Timeout`。

当 `delay` 大于 `2147483647` 或小于 `1` 时，`delay` 会被设为 `1`。

如果 `callback` 不是一个函数，则抛出 [`TypeError`]。

