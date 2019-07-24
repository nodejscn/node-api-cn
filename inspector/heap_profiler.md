
Here's an example showing how to use the [Heap Profiler][]:

```js
const inspector = require('inspector');
const fs = require('fs');
const session = new inspector.Session();

const fd = fs.openSync('profile.heapsnapshot', 'w');

session.connect();

session.on('HeapProfiler.addHeapSnapshotChunk', (m) => {
  fs.writeSync(fd, m.params.chunk);
});

session.post('HeapProfiler.takeHeapSnapshot', null, (err, r) => {
  console.log('Runtime.takeHeapSnapshot done:', err, r);
  session.disconnect();
  fs.closeSync(fd);
});
```







