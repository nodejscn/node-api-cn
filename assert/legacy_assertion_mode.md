

传统的断言模式在以下方法中使用[抽象的相等性比较][Abstract Equality Comparison]：

* [`assert.deepEqual()`][]
* [`assert.equal()`][]
* [`assert.notDeepEqual()`][]
* [`assert.notEqual()`][]

使用传统的断言模式：

```js
const assert = require('assert');
```

只要有可能，请使用[严格的断言模式][strict assertion mode]。 
否则，[抽象的相等性比较][Abstract Equality Comparison]可能会导致意外的结果。
特别是对于 [`assert.deepEqual()`]，其中的比较规则是松散的：

```js
assert.deepEqual(/a/gi, new Date());
```

