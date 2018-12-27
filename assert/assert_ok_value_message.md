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
相当于 `assert.equal(!!value, true, message)`。

如果 `value` 不为真值，则抛出 `AssertionError`。

```js
const assert = require('assert').strict;

assert.ok(true);
// 测试通过。
assert.ok(1);
// 测试通过。

assert.ok();
// 抛出 AssertionError: No value argument passed to `assert.ok()`

assert.ok(false, '不是真值');
// 抛出 AssertionError: 不是真值

// 在 repl 中：
assert.ok(typeof 123 === 'string');
// 抛出 AssertionError: false == true

// 在文件中（例如 test.js）：
assert.ok(typeof 123 === 'string');
// 抛出 AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(typeof 123 === 'string')
assert.ok(false);
// 抛出 AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(false)

assert.ok(0);
// 抛出 AssertionError: The expression evaluated to a falsy value:
//
//   assert.ok(0)

// 等同于 `assert()`：
assert(0);
// 抛出 AssertionError: The expression evaluated to a falsy value:
//
//   assert(0)
```


