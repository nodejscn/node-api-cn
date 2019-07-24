<!-- YAML
added: v0.1.21
-->
* `message` {string|Error} **默认值:** `'Failed'`。

使用提供的错误消息或默认错误消息抛出 `AssertionError`。 
如果 `message` 参数是 [`Error`] 的实例，则它将被抛出而不是 `AssertionError`。


```js
const assert = require('assert').strict;

assert.fail();
// AssertionError [ERR_ASSERTION]: Failed

assert.fail('失败');
// AssertionError [ERR_ASSERTION]: 失败

assert.fail(new TypeError('需要数组'));
// TypeError: 需要数组
```

使用带有两个以上参数的 `assert.fail()` 是可能的，但已弃用。 
请参阅下文了解更多详情。


