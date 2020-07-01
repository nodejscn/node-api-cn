<!-- YAML
added: v0.1.26
changes:
  - version:
     - v13.4.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/27867
    description: Added captureRejections option.
-->

`EventEmitter` 类由 `events` 模块定义和公开：

```js
const EventEmitter = require('events');
```

当添加新的监听器时，所有 `EventEmitter` 都会触发 `'newListener'` 事件；当移除现有的监听器时，则触发 `'removeListener'` 事件。

它支持以下选项：

* `captureRejections` {boolean} 它可以[自动捕获 promise 的拒绝][capturerejections]。 **默认值:** `false`。

