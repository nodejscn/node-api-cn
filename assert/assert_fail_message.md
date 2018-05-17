<!-- YAML
added: v0.1.21
-->
* `message` {any} 默认为 `'Failed'`。

抛出 `AssertionError`，并带上提供的错误信息或默认的错误信息。
如果 `message` 参数是 [`Error`] 的实例，则会抛出它而不是 `AssertionError`。

```js
const assert = require('assert').strict;

assert.fail();
// 抛出 AssertionError [ERR_ASSERTION]: Failed

assert.fail('失败');
// 抛出 AssertionError [ERR_ASSERTION]: 失败

assert.fail(new TypeError('失败'));
// 抛出 TypeError: 失败
```

使用 `assert.fail()` 并带上多个参数的方法已被废弃。

