<!-- YAML
added: v0.1.21
-->
* `actual` {any}
* `expected` {any}
* `message` {any}

使用[不等运算符]（`!=`）测试 `actual` 参数与 `expected` 参数是否不相等。

```js
const assert = require('assert');

assert.notEqual(1, 2);
// 测试通过。

assert.notEqual(1, 1);
// 抛出 AssertionError: 1 != 1

assert.notEqual(1, '1');
// 抛出 AssertionError: 1 != '1'
```

如果两个值相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。

