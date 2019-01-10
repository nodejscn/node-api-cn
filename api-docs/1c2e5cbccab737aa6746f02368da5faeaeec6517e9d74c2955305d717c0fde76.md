<!-- YAML
added: v0.1.26
-->

`EventEmitter` 类由 `events` 模块定义：

```js
const EventEmitter = require('events');
```

当新增监听器时，会触发 `'newListener'` 事件；当移除已存在的监听器时，则触发 `'removeListener'` 事件。

