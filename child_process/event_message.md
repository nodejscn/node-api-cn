<!-- YAML
added: v0.5.9
-->

* `message` {Object} a parsed JSON object or primitive value.
* `sendHandle` {Handle} a [`net.Socket`][] or [`net.Server`][] object, or
  undefined.

The `'message'` event is triggered when a child process uses [`process.send()`][]
to send messages.

