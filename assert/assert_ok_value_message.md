<!-- YAML
added: v0.1.21
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18319
    description: The `assert.ok()` (no arguments) will now use a predefined
                 error message.
-->
* `value` {any}
* `message` {string|Error}

测试 `value` 是否为真值。
等同于 `assert.equal(!!value, true, message)`。

如果 `value` 不是真值，则抛出 `AssertionError`，并将 `message` 属性设置为等于 `message` 参数的值。
如果未定义 `message` 参数，则会分配默认错误消息。
如果 `message` 参数是 [`Error`] 的实例，则它将被抛出而不是 `AssertionError`。
如果没有传入任何参数，则将 `message` 设置为字符串：``'No value argument passed to `assert.ok()`'``。

注意，在 `repl` 中，错误消息将与文件中抛出的错误消息不同！请参阅下文了解更多详情。

```js
const assert = require('assert').strict;

assert.ok(true);
// OK
assert.ok(1);
// OK

assert.ok();
// AssertionError: No value argument passed to `assert.ok()`

assert.ok(false, '这是假值');
// AssertionError: 这是假值

// 在 repl 中：
assert.ok(typeof 123 === 'string');
// AssertionError: false == true

// 在文件中（例如 test.js）：
assert.ok(typeof 123 === 'string');
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(typeof 123 === 'string')

assert.ok(false);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(false)

assert.ok(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(0)

// 与使用 `assert()` 相同：
assert(0);
// AssertionError: The expression evaluated to a falsy value:
//
//   assert(0)
```


