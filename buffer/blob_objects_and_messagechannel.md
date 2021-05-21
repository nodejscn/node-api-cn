
Once a {Blob} object is created, it can be sent via `MessagePort` to multiple
destinations without transferring or immediately copying the data. The data
contained by the `Blob` is copied only when the `arrayBuffer()` or `text()`
methods are called.

```js
const { Blob } = require('buffer');
const blob = new Blob(['hello there']);
const { setTimeout: delay } = require('timers/promises');

const mc1 = new MessageChannel();
const mc2 = new MessageChannel();

mc1.port1.onmessage = async ({ data }) => {
  console.log(await data.arrayBuffer());
  mc1.port1.close();
};

mc2.port1.onmessage = async ({ data }) => {
  await delay(1000);
  console.log(await data.arrayBuffer());
  mc2.port1.close();
};

mc1.port2.postMessage(blob);
mc2.port2.postMessage(blob);

// The Blob is still usable after posting.
data.text().then(console.log);
```

