<!-- YAML
added: v15.4.0
-->

> Stability: 1 - Experimental

Instances of `BroadcastChannel` allow asynchronous one-to-many communication
with all other `BroadcastChannel` instances bound to the same channel name.

```js
'use strict';

const {
  isMainThread,
  BroadcastChannel,
  Worker
} = require('worker_threads');

const bc = new BroadcastChannel('hello');

if (isMainThread) {
  let c = 0;
  bc.onmessage = (event) => {
    console.log(event.data);
    if (++c === 10) bc.close();
  };
  for (let n = 0; n < 10; n++)
    new Worker(__filename);
} else {
  bc.postMessage('hello from every worker');
  bc.close();
}
```

