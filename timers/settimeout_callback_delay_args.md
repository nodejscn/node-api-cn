<!-- YAML
added: v0.0.1
-->

* `callback` {Function} 当定时器到点时要调用的函数。
* `delay` {number} 调用 `callback` 之前要等待的毫秒数。
* `...args` {any} 当调用 `callback` 时要传入的可选参数。

预定在 `delay` 毫秒之后执行的单次 `callback`。
返回一个用于 [`clearTimeout()`] 的 `Timeout`。

`callback` 可能不会精确地在 `delay` 毫秒被调用。
Node.js 不能保证回调被触发的确切时间，也不能保证它们的顺序。
回调会在尽可能接近所指定的时间上调用。

注意：当 `delay` 大于 `2147483647` 或小于 `1` 时，`delay` 会被设为 `1`。

如果 `callback` 不是一个函数，则抛出 [`TypeError`]。

*Note*: This method has a custom variant for promises that is available using
[`util.promisify()`][]:

```js
const util = require('util');
const setTimeoutPromise = util.promisify(setTimeout);

setTimeoutPromise(40, 'foobar').then((value) => {
  // value === 'foobar' (passing values is optional)
  // This is executed after about 40 milliseconds.
});
```

