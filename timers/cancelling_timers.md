
[`setImmediate()`]、[`setInterval()`] 和 [`setTimeout()`] 方法每次都会返回表示预定的计时器的对象。
它们可用于取消定时器并防止触发。

It is not possible to cancel timers that were created using the promisified
variants of [`setImmediate()`][], [`setTimeout()`][].

