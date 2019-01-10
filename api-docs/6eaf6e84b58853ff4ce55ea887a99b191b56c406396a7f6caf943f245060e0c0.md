<!-- YAML
added: v0.1.104
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5901
    description: This method no longer supports multiple calls that don’t map
                 to individual `console.time()` calls; see below for details.
-->
* `label` {string}

停止之前通过调用 [`console.time()`] 启动的定时器，并打印结果到 `stdout`：

```js
console.time('100-elements');
for (let i = 0; i < 100; i++) {}
console.timeEnd('100-elements');
// 打印 100-elements: 225.438ms
```

注意：从 Node.js v6.0.0 开始，`console.timeEnd()` 删除了计时器以避免泄漏。
在旧版本上，计时器依然保留。
它允许 `console.timeEnd()` 可以多次调用同一标签。
此功能是非计划中的，不再被支持。

