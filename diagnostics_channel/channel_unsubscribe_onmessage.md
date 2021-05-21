
* `onMessage` {Function} The previous subscribed handler to remove

Remove a message handler previously registered to this channel with
[`channel.subscribe(onMessage)`][].

```js
const diagnostics_channel = require('diagnostics_channel');

const channel = diagnostics_channel.channel('my-channel');

function onMessage(message, name) {
  // Received data
}

channel.subscribe(onMessage);

channel.unsubscribe(onMessage);
```




