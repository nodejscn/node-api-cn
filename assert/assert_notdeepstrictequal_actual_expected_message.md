<!-- YAML
added: v1.2.0
-->

测试 `actual` 和 `expected` 参数是否不深度严格相等。
与 [assert.deepStrictEqual()](#assert_assert_deepstrictequal_actual_expected_message) 相反。

```js
const assert = require('assert');

assert.notDeepEqual({a:1}, {a:'1'});
// 抛出 AssertionError: { a: 1 } notDeepEqual { a: '1' }

assert.notDeepStrictEqual({a:1}, {a:'1'});
// 通过
```

如果两个值深度严格相等，则抛出一个带有 `message` 属性的 `AssertionError`，其中 `message` 属性的值等于传入的 `message` 参数的值。
如果 `message` 参数为 `undefined`，则输出默认的错误信息。

