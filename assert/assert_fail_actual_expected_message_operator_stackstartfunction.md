<!-- YAML
added: v0.1.21
-->
* `actual` {any}
* `expected` {any}
* `message` {any}
* `operator` {string} (默认: '!=')
* `stackStartFunction` {function} (default: `assert.fail`)

抛出 `AssertionError`。
如果 `message` 不存在，则错误信息会被设为 `actual` 的值加分隔符 `operator` 再加 `expected` 的值。
If just the two `actual` and `expected` arguments are provided, `operator` will
default to `'!='`. If `message` is provided only it will be used as the error
message, the other arguments will be stored as properties on the thrown object.
If `stackStartFunction` is provided, all stack frames above that function will
be removed from stacktrace (see [`Error.captureStackTrace`]).

```js
const assert = require('assert');

assert.fail(1, 2, undefined, '>');
// 抛出 AssertionError [ERR_ASSERTION]: 1 > 2

assert.fail(1, 2, '失败');
// 抛出 AssertionError [ERR_ASSERTION]: 失败

assert.fail(1, 2, '错误信息', '>');
// 抛出 AssertionError [ERR_ASSERTION]: 错误信息
```

*Note*: Is the last two cases `actual`, `expected`, and `operator` have no
influence on the error message.

```js
assert.fail();
// AssertionError [ERR_ASSERTION]: Failed

assert.fail('错误信息');
// 抛出 AssertionError [ERR_ASSERTION]: 错误信息

assert.fail('a', 'b');
// 抛出 AssertionError [ERR_ASSERTION]: 'a' != 'b'
```

Example use of `stackStartFunction` for truncating the exception's stacktrace:
```js
function suppressFrame() {
  assert.fail('a', 'b', undefined, '!==', suppressFrame);
}
suppressFrame();
// AssertionError [ERR_ASSERTION]: 'a' !== 'b'
//     at repl:1:1
//     at ContextifyScript.Script.runInThisContext (vm.js:44:33)
//     ...
```

