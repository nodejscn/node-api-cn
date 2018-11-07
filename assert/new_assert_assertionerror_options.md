<!-- YAML
added: v0.1.21
-->
* `options` {Object}
  * `message` {string} 如果有值，则错误信息会被设为该值。
  * `actual` {any} 错误实例的 `actual` 属性会被设为该值。
     用于 `actual` 的错误输入，例如使用 [`assert.strictEqual()`]。
  * `expected` {any} 错误实例的 `expected` 属性会被设为该值。
     用于 `expected` 的错误输入，例如使用 [`assert.strictEqual()`]。
  * `operator` {string} 错误实例的 `operator` 属性会被设为该值。
     用于表明比较时使用的是哪个操作（或触发错误的是哪个断言函数）。
  * `stackStartFn` {Function} 如果有值，则由提供的函数生成堆栈踪迹。

`Error` 的一个子类，表明断言的失败。

所有实例都包含内置的 `Error` 属性（`message` 和 `name`）以及：

* `actual` {any} 被设为实际值，例如使用 [`assert.strictEqual()`]。
* `expected` {any} 被设为期望值，例如使用 [`assert.strictEqual()`]。
* `generatedMessage` {boolean} 表明信息是否为自动生成的。
* `code` {string} 总是被设为 `ERR_ASSERTION`，表明错误是一个断言错误。
* `operator` {string} 被设为传入的运算符的值。

```js
const assert = require('assert');

// 生成一个 AssertionError，用于比较错误信息：
const { message } = new assert.AssertionError({
  actual: 1,
  expected: 2,
  operator: 'strictEqual'
});

// 验证输出的错误：
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

