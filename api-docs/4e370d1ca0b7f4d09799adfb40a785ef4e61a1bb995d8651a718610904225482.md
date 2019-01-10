<!-- YAML
added: v0.1.21
-->
* `options` {Object}
  * `message` {string} 如果指定，则作为错误的信息。
  * `actual` {any} 指定错误实例的 `actual` 属性。
  * `expected` {any} 指定错误实例的 `expected` 属性。
  * `operator` {string} 指定错误实例的 `operator` 属性。表明使用的对比操作（或触发错误的断言方法）。
  * `stackStartFn` {Function} 如果指定，则由提供的函数生成堆栈踪迹。

`Error` 的子类，表明断言的失败。

所有实例都包含内置的 `Error` 属性（`message` 和 `name`）以及：

* `actual` {any} 实际值。
* `expected` {any} 期望值。
* `generatedMessage` {boolean} 是否自动生成信息。
* `code` {string} 总是为 `ERR_ASSERTION`，表明是断言错误。
* `operator` {string} 运算符。

```js
const assert = require('assert');

// 创建一个 AssertionError，用于对比错误：
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual'
});

// 校验错误：
try {
  assert.strictEqual(1, 2);
} catch (err) {
  assert(err instanceof assert.AssertionError);
  assert.strictEqual(err.message, message);
  assert.strictEqual(err.name, 'AssertionError [ERR_ASSERTION]');
  assert.strictEqual(err.actual, 1);
  assert.strictEqual(err.expected, 2);
  assert.strictEqual(err.code, 'ERR_ASSERTION');
  assert.strictEqual(err.operator, 'strictEqual');
  assert.strictEqual(err.generatedMessage, true);
}
```

