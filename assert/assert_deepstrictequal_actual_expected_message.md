<!-- YAML
added: v1.2.0
-->

大多数情况下等同于 `assert.deepEqual()`，但有两个例外。
首先，原始值使用严格相等运算符（`===`）进行比较。
其次，对象对比包括严格比较它们的原型。

```js
const assert = require('assert');

assert.deepEqual({a:1}, {a:'1'});
// 通过，因为 1 == '1'

assert.deepStrictEqual({a:1}, {a:'1'});
// 抛出 AssertionError: { a: 1 } deepStrictEqual { a: '1' }
// 因为 1 !== '1' 使用严格相等运算符
```

如果两个值不相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则输出默认的错误信息。

