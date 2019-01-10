
[`setImmediate()`]、[`setInterval()`] 和 [`setTimeout()`] 方法每次都会返回表示预定的计时器的对象。
它们可用于取消定时器并防止触发。

不可能取消使用[`setImmediate()`][]，[`setTimeout()`][]的promisified变体创建的定时器。

