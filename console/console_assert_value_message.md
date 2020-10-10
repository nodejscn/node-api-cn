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


如果 `value` 为[非真][falsy]或省略，则 `console.assert()` 会写入消息。 
它只写入消息，不影响执行。 
输出始终以 `"Assertion failed"` 开头。 
如果提供了 `message`，则使用 [`util.format()`] 格式化它。

如果 `value` 为[真][truthy]，则什么也不会发生。

```js
console.assert(true, '什么都不做');

console.assert(false, '%s 工作', '无法');
// Assertion failed: 无法工作

console.assert();
// Assertion failed
```


