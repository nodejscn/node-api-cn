<!-- YAML
added: v0.1.26
changes:
  - version:
     - v13.4.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/27867
    description: 添加了 captureRejections 选项。
-->

`EventEmitter` 类由 `events` 模块定义和公开：

```js
const EventEmitter = require('events');
```

当有新的监听器被添加时，所有 `EventEmitter` 都会触发 `'newListener'` 事件；当现有的监听器被移除时，则触发 `'removeListener'` 事件。

它支持以下选项：

* `captureRejections` {boolean} 可启用[自动捕获 promise 的拒绝][capturerejections]。 **默认值:** `false`。


