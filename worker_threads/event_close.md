<!-- YAML
added: v10.5.0
-->

The `'close'` event is emitted once either side of the channel has been
disconnected.

```js
const { MessageChannel } = require('worker_threads');
const { port1, port2 } = new MessageChannel();

// Prints:
//   foobar
//   closed!
port2.on('message', (message) => console.log(message));
port2.on('close', () => console.log('closed!'));

port1.postMessage('foobar');
port1.close();
```

