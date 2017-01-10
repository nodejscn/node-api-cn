<!-- YAML
added: v0.1.26
-->

The `EventEmitter` class is defined and exposed by the `events` module:

```js
const EventEmitter = require('events');
```

All EventEmitters emit the event `'newListener'` when new listeners are
added and `'removeListener'` when existing listeners are removed.

