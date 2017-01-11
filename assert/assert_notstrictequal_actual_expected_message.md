<!-- YAML
added: v0.1.21
-->

使用严格不等运算符（`!==`）来测试 `actual` 和 `expected` 参数是否不严格相等。

```js
const assert = require('assert');

assert.notStrictEqual(1, 2);
// 通过

assert.notStrictEqual(1, 1);
// 抛出 AssertionError: 1 !== 1

assert.notStrictEqual(1, '1');
// 通过
```

如果两个值严格相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则输出默认的错误信息。

