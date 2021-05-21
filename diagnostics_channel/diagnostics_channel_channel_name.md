
* `name` {string|symbol} The channel name
* Returns: {Channel} The named channel object

This is the primary entry-point for anyone wanting to interact with a named
channel. It produces a channel object which is optimized to reduce overhead at
publish time as much as possible.

```js
const diagnostics_channel = require('diagnostics_channel');

const channel = diagnostics_channel.channel('my-channel');
```

