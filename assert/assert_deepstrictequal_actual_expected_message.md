<!-- YAML
added: v1.2.0
-->

大多数情况下与 `assert.deepEqual()` 一样，但有两个例外。
首先，原始值使用全等运算符（`===`）比较。
其次，对象的比较包括检查它们的原型是否全等。

```js
const assert = require('assert');

assert.deepEqual({a:1}, {a:'1'});
// 通过，因为 1 == '1'

assert.deepStrictEqual({a:1}, {a:'1'});
// 抛出 AssertionError: { a: 1 } deepStrictEqual { a: '1' }
// 因为 1 !== '1' 使用全等运算符
```

如果两个值不相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则赋予默认的错误信息。

