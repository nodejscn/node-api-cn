<!-- YAML
added: v0.9.2
-->

The `'newSession'` event is emitted upon creation of a new TLS session. This may
be used to store sessions in external storage. The listener callback is passed
three arguments when called:

* `sessionId` - The TLS session identifier
* `sessionData` - The TLS session data
* `callback` {Function} A callback function taking no arguments that must be
  invoked in order for data to be sent or received over the secure connection.

*Note*: Listening for this event will have an effect only on connections
established after the addition of the event listener.

