<!-- YAML
added: v0.0.1
-->

* `callback` {Function} 当定时器到点时调用的函数。
* `delay` {number} 调用 `callback` 之前等待的毫秒数。**默认值**: `1`。
* `...args` {any} 当调用 `callback` 时传入的可选参数。
* 返回: {Timeout} 用于 [`clearTimeout()`]。

安排在 `delay` 毫秒之后执行一次性的 `callback`。

`callback` 可能不会精确地在 `delay` 毫秒后被调用 。
Node.js 不保证回调被触发的确切时间，也不保证它们的顺序。
回调会在尽可能接近指定的时间被调用。

当 `delay` 大于 `2147483647` 或小于 `1` 时，则 `delay` 将会被设置为 `1`。
非整数的 delay 会被截断为整数。

如果 `callback` 不是函数，则抛出 [`TypeError`]。

此方法有一个定制的用于 promise 的变体，使用 [`util.promisify()`] 创建：

```js
const util = require('util');
const setTimeoutPromise = util.promisify(setTimeout);

setTimeoutPromise(40, 'foobar').then((value) => {
  // value === 'foobar' （传值是可选的）
  // 这会在大约 40 毫秒后执行。
});
```

