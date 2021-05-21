
Following is a simple overview of the public API.

```js
const diagnostics_channel = require('diagnostics_channel');

// Get a reusable channel object
const channel = diagnostics_channel.channel('my-channel');

// Subscribe to the channel
channel.subscribe((message, name) => {
  // Received data
});

// Check if the channel has an active subscriber
if (channel.hasSubscribers) {
  // Publish data to the channel
  channel.publish({
    some: 'data'
  });
}
```

