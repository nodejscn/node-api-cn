<!-- YAML
added: v0.9.3
changes:
  - version: v6.1.0, v4.7.0
    pr-url: https://github.com/nodejs/node/pull/6394
    description: For listeners attached using `.once()`, the `listener` argument
                 now yields the original listener function.
-->

* `eventName` {any} 事件名
* `listener` {Function} 事件句柄函数

`'removeListener'` 事件在 `listener` 被移除后触发。

