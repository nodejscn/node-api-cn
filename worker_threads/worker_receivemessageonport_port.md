<!-- YAML
added: v12.3.0
changes:
  - version: v15.12.0
    pr-url: https://github.com/nodejs/node/pull/37535
    description: The port argument can also refer to a `BroadcastChannel` now.
-->

* `port` {MessagePort|BroadcastChannel}

* Returns: {Object|undefined}

Receive a single message from a given `MessagePort`. If no message is available,
`undefined` is returned, otherwise an object with a single `message` property
that contains the message payload, corresponding to the oldest message in the
`MessagePort`’s queue.

```js
const { MessageChannel, receiveMessageOnPort } = require('worker_threads');
const { port1, port2 } = new MessageChannel();
port1.postMessage({ hello: 'world' });

console.log(receiveMessageOnPort(port2));
// Prints: { message: { hello: 'world' } }
console.log(receiveMessageOnPort(port2));
// Prints: undefined
```

When this function is used, no `'message'` event is emitted and the
`onmessage` listener is not invoked.

