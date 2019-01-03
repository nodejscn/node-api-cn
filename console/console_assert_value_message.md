<!-- YAML
added: v0.1.101
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17706
    description: The implementation is now spec compliant and does not throw
                 anymore.
-->
* `value` {any} The value tested for being truthy.
* `...message` {any} All arguments besides `value` are used as error message.

一个简单的断言测试，验证 `value` 是否为真。
如果不为真，则抛出 `AssertionError`。
如果提供了 `message`，则使用 [`util.format()`] 格式化并作为错误信息使用。

```js
console.assert(true, 'does nothing');
// 通过
console.assert(false, 'Whoops %s', 'didn\'t work');
// AssertionError: Whoops didn't work
```

