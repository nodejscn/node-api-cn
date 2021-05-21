
* `onMessage` {Function} The handler to receive channel messages
  * `message` {any} The message data
  * `name` {string|symbol} The name of the channel

Register a message handler to subscribe to this channel. This message handler
will be run synchronously whenever a message is published to the channel. Any
errors thrown in the message handler will trigger an [`'uncaughtException'`][].

```js
const diagnostics_channel = require('diagnostics_channel');

const channel = diagnostics_channel.channel('my-channel');

channel.subscribe((message, name) => {
  // Received data
});
```

