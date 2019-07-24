
> 稳定性: 0 - 废弃: 改为使用严格模式。

当直接访问 `assert` 而不是使用 `strict` 属性时，将对名称中没有 "strict" 的任何函数（例如 [`assert.deepEqual()`]）使用[抽象的相等性比较][Abstract Equality Comparison]。

它可以使用以下方式访问：

```js
const assert = require('assert');
```


建议使用[严格模式][`strict mode`]，因为[抽象的相等性比较][Abstract Equality Comparison]通常会产生意外的结果。 
特别是对于 [`assert.deepEqual()`]，其中的比较规则是松散的：


```js
// 注意：这不会抛出 AssertionError！
assert.deepEqual(/a/gi, new Date());
```

