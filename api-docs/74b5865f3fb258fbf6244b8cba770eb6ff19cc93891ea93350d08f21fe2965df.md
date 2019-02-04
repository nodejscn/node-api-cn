<!-- YAML
added: v0.1.101
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17706
    description: The implementation is now spec compliant and does not throw
                 anymore.
-->
* `value` {any} 测试是否为真的值。
* `...message` {any} 除 `value` 之外的所有参数都用作错误消息。

一个简单的断言测试，用于验证 `value` 是否为真。 
如果不是，则记录 `Assertion failed`。 
如果提供 `message`，则通过传入所有消息参数来使用 [`util.format()`] 格式化错误消息。 
输出用作错误消息。

```js
console.assert(true, '什么都不做');
// OK
console.assert(false, '%s 工作', '无法');
// Assertion failed: 无法工作
```

使用非真的断言调用 `console.assert()` 只会导致打印 `message` 到控制台而不会中断后续代码的执行。

