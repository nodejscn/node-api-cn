<!-- YAML
added: v0.1.21
-->
* `actual` {any}
* `expected` {any}
* `message` {any}
* `operator` {string} 默认为 `'!='`。
* `stackStartFunction` {function} 默认为 `assert.fail`。

抛出 `AssertionError`。
如果 `message` 参数为空，则错误信息为 `actual` 参数 + `operator` 参数 + `expected` 参数。
如果只提供了 `actual` 参数与 `expected` 参数，则 `operator` 参数默认为 `'!='`。
如果提供了 `message` 参数，则它会作为错误信息，其他参数会保存在错误对象的属性中。
如果提供了 `stackStartFunction` 参数，则该函数上的栈帧都会从栈信息中移除（详见 [`Error.captureStackTrace`]）。

```js
const assert = require('assert');

assert.fail(1, 2, undefined, '>');
// 抛出 AssertionError [ERR_ASSERTION]: 1 > 2

assert.fail(1, 2, '错误信息');
// 抛出 AssertionError [ERR_ASSERTION]: 错误信息

assert.fail(1, 2, '错误信息', '>');
// 抛出 AssertionError [ERR_ASSERTION]: 错误信息
// 上面两个例子的 `actual` 参数、`expected` 参数与 `operator` 参数不影响错误消息。

assert.fail();
// 抛出 AssertionError [ERR_ASSERTION]: Failed

assert.fail('错误信息');
// 抛出 AssertionError [ERR_ASSERTION]: 错误信息

assert.fail('a', 'b');
// 抛出 AssertionError [ERR_ASSERTION]: 'a' != 'b'
```

例子，使用 `stackStartFunction` 参数拦截异常的栈信息：
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

