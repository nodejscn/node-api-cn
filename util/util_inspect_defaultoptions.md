<!-- YAML
added: v6.4.0
-->

`defaultOptions` 值允许对被 `util.inspect` 使用的默认选项进行自定义。
这对 `console.log` 或 `util.format` 等显式调用 `util.inspect` 的函数很有用。
它需被设为一个对象，包含一个或多个有效的 [`util.inspect()`] 选项。
也支持直接设置选项的属性。

```js
const util = require('util');
const arr = Array(101).fill(0);

console.log(arr); // 打印截断的数组
util.inspect.defaultOptions.maxArrayLength = null;
console.log(arr); // 打印完整的数组
```

