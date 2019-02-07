<!-- YAML
added: v0.1.21
-->
* `options` {Object}
  * `message` {string} 如果提供，则将错误消息设置为此值。
  * `actual` {any} 错误实例上的 `actual` 属性将包含此值。在内部用于 `actual` 错误输入，例如使用 [`assert.strictEqual()`]。
  * `expected` {any} 错误实例上的 `expected` 属性将包含此值。在内部用于 `expected` 错误输入，例如使用 [`assert.strictEqual()`]。
  * `operator` {string} 错误实例上的 `operator` 属性将包含此值。在内部用于表明用于比较的操作（或触发错误的断言函数）。
  * `stackStartFn` {Function} 如果提供，则生成的堆栈跟踪将移除所有帧直到提供的函数。

`Error` 的子类，表明断言的失败。

所有实例都包含内置的 `Error` 属性（`message` 和 `name`）以及：

* `actual` {any} 设置为实际值，例如使用 [`assert.strictEqual()`]。
* `expected` {any} 设置为期望值，例如使用 [`assert.strictEqual()`]。
* `generatedMessage` {boolean} 表明消息是否是自动生成的。
* `code` {string} 始终设置为字符串 `ERR_ASSERTION` 以表明错误实际上是断言错误。
* `operator` {string} 设置为传入的运算符值。

```js
const assert = require('assert');

// 生成 AssertionError 以便稍后比较错误的消息：
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual'
});

// 验证错误的输出：
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

